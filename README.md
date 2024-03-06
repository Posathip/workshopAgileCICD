name: Deploy to Firebase Hosting

on:
  push:
    branches:
      - main  # Set this to the branch you want to deploy from

jobs:
  build_and_deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js 14
      uses: actions/setup-node@v1
      with:
        node-version: '14'
    - name: Install Dependencies
      run: npm install
    - name: Deploy to Firebase
      uses: w9jds/firebase-action@master
      with:
        args: deploy --only hosting
      env:
        FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}