Para subir archivos primero tenemos que agregar los archivos que deseamos subir al repositorio, esto lo podemos realizar de las siguientes maneras:

- Agregar todos los archivos que tengas en el proyecto:
```bash
git add .
```
- Agregar archivos en especifico del proyecto:
```bash
git add my_file_2
git add my_file_5 my_file_1
git add /src/my_file_45
```

Ahora bien, para subirlos lo hacemos mediante el siguiente comando:

```bash
git commit -m "my message"
```
*Recuerda que el mensaje del commit puede tener una estructura según la manera en la que estés trabajando*

También existe una manera de agregar todos los archivos y realizar el commit al mismo tiempo:
```bash
git commit -am "my message"
```
*Esto sólo funciona con los archivos que ya has trackeado anteriormente, si hay archivos nuevos estarás forzado a utilizar a agregarlos mediante alguno de los primeros pasos*
