# Backend Development Log

- `npx create-strapi-app@latest backend`
  [create and config a new project with Strapi](https://docs.strapi.io/developer-docs/latest/getting-started/quick-start.html)
- create Products with Content-Type Builder and Content Manager
- Adding GraphQL
  `npm i @strapi/plugin-graphql`
- Configuring Setting - Roles(public) - Permissions
- Add Cloudinary support to the Strapi Application
  `npm i @strapi/provider-upload-cloudinary`
  [Cloudinary Integration](https://strapi.io/blog/add-cloudinary-support-to-your-strapi-application)
- create `plugins.js` in `./config`
  ```js
  module.exports = ({ env }) => ({
    // ...
    upload: {
      config: {
        provider: "cloudinary",
        providerOptions: {
          cloud_name: env("CLOUDINARY_NAME"),
          api_key: env("CLOUDINARY_KEY"),
          api_secret: env("CLOUDINARY_SECRET"),
        },
        actionOptions: {
          upload: {},
          delete: {},
        },
      },
    },
    // ...
  });
  ```
- update `middlewares.js` in `./config`

  ```js
  module.exports = [
    "strapi::errors",
    {
      name: "strapi::security",
      config: {
        contentSecurityPolicy: {
          useDefaults: true,
          directives: {
            "connect-src": ["'self'", "https:"],
            "img-src": ["'self'", "data:", "blob:", "res.cloudinary.com"],
            "media-src": ["'self'", "data:", "blob:", "res.cloudinary.com"],
            upgradeInsecureRequests: null,
          },
        },
      },
    },
    "strapi::cors",
    "strapi::poweredBy",
    "strapi::logger",
    "strapi::query",
    "strapi::body",
    "strapi::session",
    "strapi::favicon",
    "strapi::public",
  ];
  ```

- setup `.env`
  ```
  CLOUDINARY_NAME=
  CLOUDINARY_KEY=
  CLOUDINARY_SECRET=
  ```
