name: Deploy Minecraft Server

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Docker
      uses: docker/setup-buildx-action@v1

    - name: Build Docker image
      run: docker build -t minecraft-server .

    - name: Run Minecraft Server
      run: docker run -d -p 25565:25565 minecraft-server
