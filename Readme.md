asdfasdname: CI/CD Pipeline

on:
  push:
    branches:
      - develop
      - main

jobs:
  build-test-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repositorio
        uses: actions/checkout@v3

      - name: Instalar dependencias
        run: npm install

      - name: Ejecutar pruebas
        run: npm test

      - name: Compilar proyecto
        run: npm run build

      - name: Deploy a Staging
        if: github.ref == 'refs/heads/develop'
        run: echo "🚀 Desplegando en Staging..."

      - name: Deploy a Producción
        if: github.ref == 'refs/heads/main'
        run: echo "🚀 Desplegando en Producción..."
