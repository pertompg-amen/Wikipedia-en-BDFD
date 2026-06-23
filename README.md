# 📖 Wikipedia Command — Bot Designer For Discord

> Comando `!wiki` para buscar artículos de Wikipedia en español directamente desde Discord, con embed enriquecido y thumbnail automático.

---

## 📋 Requisitos

| Requisito | Detalle |
|-----------|---------|
| 📱 App | [Bot Designer For Discord (BDFD)](https://botdesignerdiscord.com/) |
| 📝 Lenguaje | BdScript 2 |
| 🌐 Acceso a internet | Requerido para las llamadas HTTP |
| 🔑 Permisos del bot | `Send Messages`, `Embed Links` |

> [!IMPORTANT]
> Este comando está escrito en **BdScript 2**. Asegúrate de seleccionar ese lenguaje al crear el comando en BDFD, de lo contrario las funciones no funcionarán correctamente.

---

## 🚀 Instalación

1. Abre **Bot Designer For Discord**
2. Ve a tu bot → **Commands** → **Add Command**
3. Configura el trigger: `!wiki`
4. Selecciona el lenguaje: **BdScript 2**
5. Pega el código de abajo
6. Guarda y prueba con `!wiki La Nobleza De Las Flores` (soy inocente)

---

## 🧾 Código

```python
$nomention
$botTyping
$httpGet[https://es.wikipedia.org/api/rest_v1/page/summary/$replaceText[$message; ;_]]
$var[esStatus;$httpStatus]
$var[title;$httpResult[title]]
$var[extract;$httpResult[extract]]
$httpGet[https://en.wikipedia.org/api/rest_v1/page/summary/$replaceText[$message; ;_]]
$var[thumb;$httpResult[thumbnail;source]]

$if[$var[esStatus]==400]
$description[❌ El término de búsqueda contiene caracteres inválidos.]
$color[ff0000]
$elseif[$var[esStatus]==404]
$description[❌ No encontré ningún artículo en Wikipedia que coincida con tu búsqueda.]
$color[ff0000]
$else
$title[$var[title]]
$description[$var[extract]]
$thumbnail[$var[thumb]]
$color[00FF00]
$endif
```

---


## 🛑 Manejo de errores

| Código HTTP | Causa | Respuesta del bot |
|-------------|-------|-------------------|
| `400` | Título con caracteres inválidos |
| `404` | Artículo no existe en Wikipedia ES |

> [!NOTE]
> El thumbnail se obtiene de **Wikipedia en inglés** porque muchos artículos en español (especialmente de anime/manga) son stubs y no tienen imagen asignada. Si el artículo tampoco tiene imagen en inglés, el embed simplemente no mostrará thumbnail, sin generar ningún error.

> [!CAUTION]
> La API de Wikipedia puede devolver textos muy largos. Discord tiene un límite de **4096 caracteres** en la descripción de un embed. Si el artículo es muy extenso, el mensaje puede fallar o cortarse.

---

## 📌 Ejemplo de uso

```
!wiki Código de Hammurabi
!wiki Agujero negro
!wiki One Piece
```

> [!WARNING]
> No uses el comando con términos demasiado genéricos como `!wiki a` o `!wiki 123`. La API puede devolver resultados inesperados o errores de redirección.

---

## 📸 Vista previa

<div align="center">
  <img src="https://i.ibb.co/VY8QsqXH/Screenshot-20260623-191822-Discord.jpg" alt="Vista previa del comando !wiki en Discord" width="400"/>
  <br/>
  <sub>⬆️ Resultado del comando <code>!wiki La Nobleza De Las Flores</code> en Discord</sub>
</div>

---

## 📚 Referencias

- [Bot Designer For Discord — Wiki oficial](https://wiki.botdesignerdiscord.com/)
- [Wikipedia REST API v1 — Documentación](https://www.mediawiki.org/wiki/Wikimedia_REST_API)
- [`$httpGet` — BDFD Wiki](https://wiki.botdesignerdiscord.com/bdscript/httpGet.html)
- [`$httpResult` — BDFD Wiki](https://wiki.botdesignerdiscord.com/bdscript/httpResult.html)
- [`$var` — BDFD Wiki](https://wiki.botdesignerdiscord.com/bdscript/var.html)

---

## 📄 Licencia

Este proyecto está bajo la licencia **MIT**. Puedes usar, modificar y distribuir el código libremente.

---

<div align="center">
  Hecho con ❤️ para la comunidad BDS World :D
</div>
