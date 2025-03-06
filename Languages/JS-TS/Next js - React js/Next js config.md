
___
```TS
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  images: {
    domains: [process.env.SERVER_DOMAIN!], // domian images
  },

  async rewrites() { // rewrites
    return [
      {
        source: `/uploads/:path*`,
        destination: `${process.env.IMAGE_URL}/:path*`,
      },
    ]
  },
}

export default nextConfig

```