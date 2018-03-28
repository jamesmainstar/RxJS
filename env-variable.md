"export NODE_ENV=development && npm run build"

'process.env.NODE_ENV': `"${config.util.getEnv('NODE_ENV')}"`