## Script en Python para la descarga de los libros de Springer publicados de manera gratuita durante la cuarentena del COVID-19 de 2020

### Usage
**Note**: If you want just one or two specific books, get the excel file [here](https://resource-cms.springernature.com/springer-cms/rest/v1/content/17858272/data/v4) and manually download those or use the script to help you download (see **Download book selectively** sub-section). It took about 4 hours to complete the 409 english books (14 GB, both PDF and EPUB) on my machine.

Por defecto el script almacena los libros en el directorio `./downloads` y en subcarpetas acorde al asunto (ver columna del fichero excel "English Package Name").

#### Descarga de todos los libros (Formatos: PDF y EPUB)
Use the following command to download all PDF and EPUB books to the default download folder `./downloads`
```bash
python3 main.py
```
To download them to a subfolder of your choice, say `books`
```bash
python3 main.py -f ./books
```
You can download to an absolute path, say `C:/ebooks/springer/`
```bash
python3 main.py -f C:/ebooks/springer/
```

#### Descarga de todos los libros en un formato especifico
To download all PDF books only, run
```bash
python3 main.py --pdf
```
or all EPUB books only
```bash
python3 main.py --epub
```

#### Descarga de una categoria de libros
You can download selective books by categories. Make sure category name with space(s) is enclosed in double quotation marks,  like so
```bash
python3 main.py -c Enginnering "CoMpuTer sciEnCe"
```
The category name is case-insensitive.

#### Descarga de una selección de libros
You can download books by indices (refer to the excel file for the titles)
```bash
python3 main.py -i 2 345 70 90 0 213
```

#### Modo Verbose
If you need to know what you are downloading, enable the verbose mode with `-v` option
```bash
python3 main.py -v -c "Behavioral science and psychology" "chaos AD" UFO "Life science" -i 2 34 400
```
You will get the following summary before the downloading starts
```
                                          Book Title               English Package Name
2                                  All of Statistics         Mathematics and Statistics
34                            Essential Astrophysics              Physics and Astronomy
37       International Perspectives on Psychotherapy  Behavioral Science and Psychology
40                         Applied Behavior Analysis  Behavioral Science and Psychology
70                          Psychology of Perception  Behavioral Science and Psychology
95             Handbook of Consumer Finance Research  Behavioral Science and Psychology
311       Clinical Methods in Medical Family Therapy  Behavioral Science and Psychology
313                           Motivation and Action   Behavioral Science and Psychology
381                          Perceptual Organization  Behavioral Science and Psychology
396  Evidence-Based Practice in Clinical Social Work  Behavioral Science and Psychology
397                 Foundations of Behavioral Health  Behavioral Science and Psychology
398                      Social Psychology in Action  Behavioral Science and Psychology
400             A Course in Rasch Measurement Theory                          Education

13 titles ready to be downloaded...
The following invalid book categories will be ignored:
 1. chaos AD
 2. UFO
 3. Life science
```

### Ejecución en un entorno virtual:

```bash
python3 -m venv .venv
. .venv/bin/activate
pip install -r requirements.txt
python3 main.py
```

### Virtual environment on Windows (Python 3.x):

```bash
python -m venv .venv
.venv\Scripts\activate.bat
pip install -r requirements.txt
python main.py
```

### Virtual environment on Windows (Python 2.7.x):
```bash
python -m virtualenv .venv
.venv\Scripts\activate.bat
pip install -r requirements2x.txt
python main.py
```



### Source:
* https://group.springernature.com/gp/group/media/press-releases/freely-accessible-textbook-initiative-for-educators-and-students/17858180?utm_medium=social&utm_content=organic&utm_source=facebook&utm_campaign=SpringerNature_&sf232256230=1
* https://www.springernature.com/gp/librarians/news-events/all-news-articles/industry-news-initiatives/free-access-to-textbooks-for-institutions-affected-by-coronaviru/17855960
* https://resource-cms.springernature.com/springer-cms/rest/v1/content/17858272/data/v4

Thanks Springer!

## Docker container to do all the work

Considering you cloned the repo in a folder, as:
```bash
cd \home\[user]\workspace`
git clone https://github.com/alexgand/springer_free_books.git
cd springer_free_books
mkdir downloads
```

You can run the scripts like that:
```bash
docker build . -t springer-image
docker run --rm -v [local_download_folder]:/app/downloads springer-image
```
and the downloads will be at [`local_download_folder`].
