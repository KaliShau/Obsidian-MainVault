
___
```TS
import axios, { CreateAxiosDefaults } from 'axios'
import { SERVER_URL } from '../config/api.config'
import { errorCatch, getContentType } from './api.helper'
import { cookiesTokens } from '../utils/token.utils'
import { AuthService } from '../services/auth.service'

const options: CreateAxiosDefaults = {
  baseURL: `${SERVER_URL}/api`,
  headers: getContentType(),
  withCredentials: true,
}

export const axiosClassic = axios.create(options)
export const axiosWithAuth = axios.create(options)

axiosWithAuth.interceptors.response.use(config => {
  const accessToken = cookiesTokens.getAccessToken()

  if (config?.headers && accessToken)
    config.headers.Authorization = `Bearer ${accessToken}`

  return config
})

axiosWithAuth.interceptors.request.use(
  config => config,
  async error => {
    const originalRequest = error.config

    if (
      (error?.response?.status == 401 ||
        errorCatch(error) === 'jwt expired' ||
        errorCatch(error) === 'jwt must be provided') &&
      error.config &&
      !error.config._isRetry
    ) {
      originalRequest._isRetry = true
      try {
        await AuthService.getNewTokens()
        return axiosWithAuth.request(originalRequest)
      } catch (error) {
        if (errorCatch(error) === 'jwt expired')
          cookiesTokens.removeAccessToken()
      }
    }

    throw error
  }
)

```