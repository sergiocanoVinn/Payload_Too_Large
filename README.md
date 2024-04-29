# API: 413 Payload_Too_Large 

## Solucion al error API: 413

<img src="https://raw.githubusercontent.com/sergiocanoVinn/Payload_Too_Large/main/imgs/zz.png">

Cuando se presente este error lo que tenemos que hacer comunmente es correr manualmente el comando 

```bash
vtex link 
```
pero cuando este error se presenta seguido esto se vuelve un poco tedioso.

Entonces para evitarnos esto podemos crear un script que ejecute el vtex link 
y si detecte un error que lo vuelva a ejecutar. Este script lo podemos crear a raiz
de nuestro proyecto (al nivel del package.json), con el nombre link.js

```js
const { exec } = require('child_process');

const runVtexLink = () => {
    console.log('Ejecutando vtex link...');
    
    const child = exec('vtex link');

    child.stdout.on('data', data => console.log(data));
    child.stderr.on('data', data => console.error(data));

    child.on('close', code  => {
        console.log(`Proceso finalizado con código ${code}`);

        if (code !== 0) {
            setTimeout(runVtexLink, 2000);
        }
    });
}

runVtexLink();

```
de esta manera ahora lo que tendremos que ejecutar seria
```bash
node link.js
```
y este ejecuta el vtex link y si detecta un error vuelve a ejecutarlo.

<img src="https://raw.githubusercontent.com/sergiocanoVinn/Payload_Too_Large/main/imgs/zzz.png">