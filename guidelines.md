## Odoo 10

### Eclipse Preferences

- General > Editors > Text Editors
  - Displayed tab width: 4
  - Inset spaces for tabs: yes
  - Show print margin: yes
  - Print margin column: 80
- PyDev > Editor > Code Analysis > Page pep8.py
  - Group "Pep8" select "Warning"
  - Use system interpreter: yes
  - Arguments: --ignore=E501
- PyDev > Editor > Tabs
  - Tab length: 4
  - Replace tabs with spaces whan typing?: yes
  - Assume tab spacing whan files contain tabs?: yes
- PyDev > Interpreters > Python Interpreter
  - Name: python, Location: /usr/bin/python
- XML > XML Files > Editor
  - Line width: 80
  - Split multiple attributes each on a new line: no
  - Align final bracket in multi-line alement tags: no
  - Preserve whitespace in tags with PCDATA content: yes
  - Clear all blank lines: no
  - Formar comments: no
  - Insert whitespace before closing empty end-tags: no
  - Ident using spaces: yes
  - Identation size: 4

### Python

#### PEP8

PEP8 es una guía de estilo para código python. En las últimas versiones desde Odoo se han esforzado en seguir el estandar de python, mejorando el código notablemente. Nosotros también lo vamos a hacer. Seguir estas recomendaciones de estilo no solo ayuda a estandarizar el código, también ayuda a su lectura, a su mantenimiento y a su posible migración a versiones posteriores de python.

Desde Eclipse hemos activado la revisión de código a excepción de los avisos por líneas demasiado largas (E501). En Odoo hay otras reglas que también se pueden saltar:

- E501: line too long
- E301: expected 1 blank line, found 0
- E302: expected 2 blank lines, found 1
- E126: continuation line over-indented for hanging indent
- E123: closing bracket does not match indentation of opening bracket's line
- E127: continuation line over-indented for visual indent
- E128: continuation line under-indented for visual indent
- E265: block comment should start with '# '

Nosotros vamos a intentar cumplir todas (es bastante sencillo) menos la E501 que nos puede costar un poco más. Esa regla límita el tamaño de cada línea a 79 caracteres. Puede que sea demasiado poco, y también que nos cueste dividir líneas muy largas en varias líneas má cortas. Aun así vamos a intentarlo. La barra vertical que sale en el editor indica el límite de linea del estandar. Si vemos que pasa de ahí intenramos acortarlo. Ante la duda de como hacer, mejor preguntar antes de dejar código que no sabemos si está bien.

Como hasta ahora no hemos aplicado estos estilos nos saldrán un monton de mensajitos de PEP8. Los típicos:
- Espacios en blanco de más o falta de algún espacio, por ejemplo entre operadores o después de los dos puntos en un diccionario
- Saltos de línea de más o de menos
- Mala tabulación del código. A veces he visto incluso tabulaciones que no son múltiplo de 4 espacios. También hay mezclas entre tabulacioens y espacios. Sólo se usarán espacios
- Variables definidas que no se usan para nada
- Imports que no se usan

#### Imports

Los import tienen que ir ordenados y agrupados en los siguientes grupos:

- Imports de librerías del core de python (un import por librería, ordenados alfabéticamente)
- Imports de Odoo (agrupados, ordenados alfabéticamente)
- Imports de otros módulos de Odoo (ordenados alfabéticamente)
- Imports de librerías de terceros (un import por librería, ordenados alfabéticamente)

Se eliminarán todos los imports que no se usen
Los imports que hagan referencia a openerp se sustituyen por el correspondiente en odoo
Los imports locales (relativos al módulo) se harán utlizando el punto como referencia. Sino estamos haciendo un import absoluto y puede dar conflictos.

Ejemplo:

    # 1 : imports of python lib
    import base64
    import re
    import time
    from datetime import datetime
    # 2 :  imports of odoo
    import odoo
    from odoo import api, fields, models, _ # alphabetically ordered
    from odoo.tools.safe_eval import safe_eval as eval
    # 3 :  imports from odoo modules
    from odoo.addons.web.controllers.main import login_redirect
    from odoo.addons.website.models.website import slug
    # 4 : imports of third party libraries
    try:
        import xmlsig
        from watchdog.observers import Observer
        from watchdog.events import PatternMatchingEventHandler
    except (ImportError, IOError):
        pass

Ejemplo de `__init__.py` del módulo:

    from . import controllers
    from . import models
    from . import wizards

Cuando estamos importando los modelos de Odoo puede que el orden sea importante. En ese caso obviar el orden alfabético y ordenar los imports según la necesidad
  
