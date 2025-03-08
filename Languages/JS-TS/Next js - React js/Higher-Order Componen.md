
___
```TS
'use client'

import { useAuth } from '@/features/get-new-tokens' 
import { PUBLIC_ROUTES } from '@/shared/config/routes.config' 
import { Loader } from '@/shared/ui/loader/loader.ui' 
import { NextPage } from 'next' 
import { redirect } from 'next/navigation' 
import { ComponentType, useEffect, useState } from 'react' 

// Создаем Higher-Order Component (HOC) для проверки авторизации
const withAuth = <P extends object>(
  WrappedComponent: ComponentType<P> 
): NextPage<P> => {
  // Возвращаем новый компонент, который будет выполнять проверку авторизации
  const AuthComponent: NextPage<P> = props => {
    // Используем хук useAuth для получения состояния авторизации и загрузки
    const { isAuth, isLoading } = useAuth()

    // Состояние для проверки, выполняется ли код на клиенте
    const [isClient, setIsClient] = useState(false)

    // useEffect для установки isClient в true после монтирования компонента
    useEffect(() => {
      setIsClient(true)
    }, [])

    // Если код еще не выполняется на клиенте или идет загрузка, показываем Loader
    if (!isClient || isLoading) {
      return <Loader />
    }

    // Если пользователь не авторизован, перенаправляем его на страницу входа
    if (!isAuth) {
      redirect(PUBLIC_ROUTES.signIn())
    }

    // Если пользователь авторизован, рендерим обернутый компонент
    return <WrappedComponent {...props} />
  }

  // Возвращаем компонент с проверкой авторизации
  return AuthComponent
}

// Экспортируем HOC для использования в других компонентах
export default withAuth
```