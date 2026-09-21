# redes-portadas

Portadas de las piezas de redes de Diego Fernández Slezak, públicas por una
razón técnica: **Meta descarga los archivos, no se le suben**. El endpoint de
publicación de reels (`POST /{ig-user-id}/media`) recibe una `cover_url` y son
los servidores de Meta los que la bajan, así que la placa necesita vivir en
algún lado que responda sin credenciales. El repo de trabajo,
`dfslezak/redes`, es privado y `raw.githubusercontent.com` le da 404.

Acá están sólo las placas terminadas, una carpeta por pieza. No están las
fuentes (`portadas/fuente/`, con fotos y capturas) ni las pruebas de armado
(los archivos `_*.png`): eso se queda en el repo privado.

## Cómo se usa

La URL es predecible:

    https://raw.githubusercontent.com/dfslezak/redes-portadas/main/<pieza>/<placa>.png

Por ejemplo:

    https://raw.githubusercontent.com/dfslezak/redes-portadas/main/2026-09-13_declaracion_ia_aula/placa-1-portada-9x16.png

Eso es lo que va en `cover_url` del `publicar.json` que consume
`_publicar/instagram.py`.

## Cómo se actualiza

Desde el repo privado, con las placas nuevas ya generadas por
`_portadas/portada.py`:

    cd ~/repos/redes
    for d in 2026-*/portadas; do
      p=${d%/portadas}
      mkdir -p ~/repos/redes-portadas/$p
      find $d -maxdepth 1 -type f -name '*.png' ! -name '_*' \
        -exec cp {} ~/repos/redes-portadas/$p/ \;
    done
    cd ~/repos/redes-portadas && git add -A && git commit -m "portadas: <pieza>" && git push

Las placas se publican igual en redes, así que no hay nada acá que no vaya a
estar a la vista de todas formas.
