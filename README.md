# GitHub Action to automate React Web build

Automate your ReactJS web build by getting help from GitHub Actions.

## GitHub Action

Config file: https://github.com/BaseMax/ReactGlobalOnlineSummit-Actions/blob/main/.github/workflows/test1.yml

```
on: push
name: 🚀 Deploy website on push
jobs:
  web-deploy:
    name: 🎉 Deploy
    runs-on: ubuntu-latest
    steps:
    - name: 🚚 Get latest code
      uses: actions/checkout@v3

    - name: Use Node.js 16
      uses: actions/setup-node@v3
      with:
        node-version: '16'
      
    - name: 🔨 Build Project
      run: |
        npm install
        npm run build
    
    - name: List output files
      run: find build/ -print
      
    - name: FTP Deployer
      uses: sand4rt/ftp-deployer@v1.4
      with:
        sftp: true
        host: asrez.com
        port: 22
        username: asrez
        password: ${{ secrets.FTP_PASSWORD }}
        remote_folder: '/home/asrez/public_html/test-react.maxbase.org/'
        local_folder: 'build/'
        cleanup: false
        include: '[ "*", "**/*" ]'
        exclude: '["node_modules/**", ".github/**", ".git/**", "*.env"]'
        pasive: true
```

Copyright 2022, Max Base
