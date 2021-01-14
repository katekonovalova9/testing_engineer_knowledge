# 1. Build tool concept

Проекты выглядят по разному в разных IDE

1) на машине которой собирается проект должна быть уставновлена IDE
2) должна использоваться IDE которая была использована
3) отсутствие поддержки камандной строки
4) dependency hell

# 2. Why Maven

- Dependency management работа со сторонними библиотеками
- build lifecycle поддержка жизненного цикла
- plugins поддержка плагинов разных

# 3. Download, install, configure

загрузить maven - maven.apache.org/download

создать переменные сред
JAVA_HOME
MAVEN_HOME
MAVEN_HOME\bin in PATH

# 4. Create project & import in IDE
сначала создать проект через командную строку и потом импортировать

Create first project from archetype

mvn archetype:generate
  -DarchetypeGroupId=org.apache.maven.archetypes
  -DarchetypeArtifactId=maven-archetype-quickstart
  -DarchetypeVersion=1.3
  
1) перейти в директорию в которой будет создан java-проект
2) вызвать командную строку и вставить строку с archetype которая выше указана
3) импортировать в ide его

# 5. Build lifecycle
Most used :
- clean очищает проект и удаляет файлы 
- test компилирует приложение и запускает unit test
- package запаковывает в бинарный файл
- install устанавливает локально в систему
- deploy деплоит на какой-то удаленный сервер

# 6. Depedency management
добавить библиотеку 

- find library at search.maven.org
- add necessary version to POM
- see it in ~/.m2/repository folder


Презентация тренинга: https://elearn.epam.com/assets/courseware/v1/3237f828d1c1b341e4a0b548389df6b7/asset-v1:EPAM+MBT+RU+type@asset+block/DevTestOps-Maven_build_tool.pdf

Официальный сайт проекта Maven: http://maven.apache.org/

Центральный maven репозиторий для поиска библиотек: https://search.maven.org/
