# Java Engine Configuration

## Properties File

> TL;DR: Call `System.setProperty("WindwardReports.properties.filename", "path/to/WindwardReports.properties")` before calling Windward and you’re good.
 
The below properties can be set most any way supported by Java properties.
Usually you will create a `WindwardReports.properties` file and point to it.
 
When Windward starts up, it makes a call to:
`String path = System.getProperty("WindwardReports.properties.filename", "WindwardReports.properties");`. It then tries to resolve that path trying
in order:

1. `Thread.currentThread().getContextClassLoader().getResource(path)`
1. `ProcessReport.class.getClassLoader().getResource(path)`
1. `ClassLoader.getSystemResource(path)`
1. `new File(path)`
1. `new URL(path)`

With the resolved resource name from the above steps, it then tries in order:

1. `Thread.currentThread().getContextClassLoader().getResourceAsStream()`
2. `ProcessReport.class.getClassLoader().getResourceAsStream()`
3. `ClassLoader.getSystemResource().openConnection().getInputStream()`
4. `new FileInputStream()`
5. `new URL().openConnection().getInputStream()`
6. `Property/Config settings

For `ImportFileClass`, see the end of this article.
 
## Configuration Settings

The below settings fall into three general categories:

1. Read in and set when the engine starts. You need to restart the engine for
   new values to be read & used. Marked as `Global`.

1. Read in and used every time a report runs. When you change these, the next
   report will use the new settings. Marked as `Local`.

1. Default values for properties you can set in a (Process)Report object. When
   you change these the next instantiation of the report object will use those
   new values as the defaults. You can then explicitly set these properties in
   the object. Marked as `Report`.

| Name               | Category | Allowed Values | Default | Description |
| ------------------ | -------- | -------------- | ------- | ----------- |
| `asian.support`    | Global | `true`, `false` | `true`  | If set to `false` then the server assumes the files needed for output of Asian text is not available and will fall-back to Latin text only` |
| `check.for.glyphs` | Local  | `on`, `off`     | `on`    | `Checks the font specified for text and changes the font if it does not have glyphs for some of the text.`   

*more here...*
