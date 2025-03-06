
___
```TS
'use client' 

import { useInfiniteQuery } from '@tanstack/react-query'
import { PostsService } from '../api/posts.service' 
import { useEffect } from 'react'
import { TypePost } from '@/shared/models/post.type' 

export const usePosts = () => {
  const limit = 2

  // Использование хука useInfiniteQuery для бесконечной подгрузки постов
  const {
    data, // Данные, полученные из запросов
    fetchNextPage, // Функция для загрузки следующей страницы данных
    hasNextPage, // Флаг, указывающий, есть ли еще данные для загрузки
    isFetchingNextPage, // Флаг, указывающий, выполняется ли загрузка следующей страницы
    isLoading, // Флаг, указывающий, выполняется ли начальная загрузка данных
    isError, // Флаг, указывающий, произошла ли ошибка при загрузке данных
    error, // Объект ошибки, если она произошла
  } = useInfiniteQuery<TypePost[]>({
    queryKey: ['posts'],
    queryFn: ({ pageParam = 1 }) => PostsService.getAll(pageParam), // Функция для выполнения запроса на получение постов
    getNextPageParam: (lastPage, allPages) => {
      // Функция для определения параметра следующей страницы
      if (lastPage.length < limit) return undefined // Если количество постов меньше лимита, следующая страница отсутствует
      return allPages.length + 1 // Возвращает номер следующей страницы
    },
    initialPageParam: 1, // Начальный параметр страницы
	})
	
	
  useEffect(() => {
    const handleScroll = () => {
      const scrollTop = document.documentElement.scrollTop // Текущая позиция прокрутки
      const scrollHeight = document.documentElement.scrollHeight // Общая высота прокручиваемого контента
      const clientHeight = document.documentElement.clientHeight // Высота видимой области окна

      const heightScroll = 100 // Расстояние от нижней границы, при котором начинается загрузка новых данных

      // Проверка, достиг ли пользователь нижней границы страницы
      if (
        scrollHeight - (scrollTop + clientHeight) <= heightScroll * 2 &&
        hasNextPage && // Проверка, есть ли еще данные для загрузки
        !isFetchingNextPage // Проверка, не выполняется ли уже загрузка следующей страницы
      ) {
        fetchNextPage() // Загрузка следующей страницы данных
      }
    }


    window.addEventListener('scroll', handleScroll)

    return () => window.removeEventListener('scroll', handleScroll)
  }, [hasNextPage, isFetchingNextPage, fetchNextPage]) 

  return {
    data,
    fetchNextPage,
    hasNextPage,
    isFetchingNextPage,
    isLoading,
    isError,
  }
}
```