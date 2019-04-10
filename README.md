We have been utilizing GATSBY_ACTIVE_ENV for setting different staging/test environments.  PR [10565](https://github.com/gatsbyjs/gatsby/pull/10565) broke none productions builds for us due to Gatsby using it internally to determine whether to fetch data in .cache/loader.  

This was an easy fix for us as we simply use another variable for determining which environments we point our site too.    
### Steps to reproduce
With gatsby-plugin-offline installed. 
GATSBY_ACTIVE_ENV=staging gatsby build
gatsby serve


### Potential solution 
In multiple places .cache/loader splits off process.env.NODE_ENV !== `production`.  Seems like process.env.NODE_ENV !== `development` would make more sense as when we are testing in staging or test it is best practice to have a build that mirrors production.
