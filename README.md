# Entorno de Elixir · Programación Lógica y Funcional

Entorno listo para usar en GitHub Codespaces: Elixir 1.20, Livebook, ElixirLS y
Dialyzer ya instalados. No hay que instalar nada en tu computadora.

## Primeros pasos

1. Arriba a la derecha: **Use this template → Create a new repository**.
   Ponle el nombre de tu equipo.
2. En **tu** repositorio nuevo: **Code → Codespaces → Create codespace on main**.
3. Espera a que abra VS Code en el navegador. La primera vez tarda un par de
   minutos mientras descarga el entorno.

Verifica que quedó:

```bash
elixir --version
```

Esa salida es la evidencia de la primera sesión.

## Uso diario

| Para | Comando |
|---|---|
| Consola interactiva | `iex` |
| Correr un archivo | `elixir archivo.exs` |
| Crear un proyecto | `mix new nombre_proyecto` |
| Correr las pruebas | `mix test` (dentro del proyecto) |
| Abrir Livebook | `livebook server` |

**Livebook** se abre solo en otra pestaña del navegador. Si no, ve a la
pestaña **Ports** de VS Code y abre el puerto 8080. Para salir: `Ctrl+C` dos veces.

**ElixirLS** (autocompletado, errores en el editor) se activa cuando abres un
proyecto creado con `mix new`. La primera vez tarda uno o dos minutos en
arrancar; es normal.

## Dialyzer

Cuando lo necesites, agrega esta línea a `deps` en el `mix.exs` de tu proyecto:

```elixir
{:dialyxir, "~> 1.4", only: [:dev, :test], runtime: false}
```

y corre:

```bash
mix deps.get
mix dialyzer
```

Cada advertencia trae una etiqueta (por ejemplo `call`). Para ver qué significa:

```bash
mix dialyzer.explain call
```

## Cuida tu cuota

Codespaces es gratuito dentro de una cuota mensual de horas.

- **Detén el codespace al terminar:** menú de VS Code (☰) → **Codespaces: Stop
  Current Codespace**, o desde https://github.com/codespaces.
- **Haz commit y push antes de irte.** Los codespaces inactivos se borran
  después de un tiempo, y lo que no subiste se pierde.

## Trabajar sin Codespaces

Con Docker instalado, la misma imagen funciona en tu computadora.

**Opción 1, VS Code:** clona tu repo, instala la extensión *Dev Containers* y
elige **Reopen in Container**.

**Opción 2, terminal** (PowerShell, parado en la carpeta de tu proyecto):

```powershell
docker run -it --rm -v ${PWD}:/app -w /app ghcr.io/tu-usuario/elixir-ide-image:2026b iex
```

En bash, WSL o macOS cambia `${PWD}` por `"$PWD"`.

Livebook desde la terminal:

```powershell
docker run -it --rm -p 8080:8080 -p 8081:8081 -e LIVEBOOK_IP=0.0.0.0 -v ${PWD}:/app -w /app ghcr.io/tu-usuario/elixir-ide-image:2026b livebook server
```

Abre la dirección que imprime, cambiando `0.0.0.0` por `localhost`.

## Si algo falla

| Síntoma | Qué hacer |
|---|---|
| El codespace no abre | Espera y recarga; si persiste, bórralo y crea otro (tu código está en GitHub si hiciste push) |
| ElixirLS no marca errores | Revisa que estés dentro de un proyecto con `mix.exs`; espera a que termine de arrancar |
| Livebook no abre | Pestaña **Ports** → puerto 8080 → abrir en el navegador |
| `mix dialyzer` tarda varios minutos | Avisa al profesor: el PLT base de la imagen no se está usando |
