```python
!pip install nltk

```

    Collecting nltk
      Downloading nltk-3.8.1-py3-none-any.whl (1.5 MB)
         ---------------------------------------- 0.0/1.5 MB ? eta -:--:--
         ---------------------------------------- 0.0/1.5 MB ? eta -:--:--
         - -------------------------------------- 0.0/1.5 MB 393.8 kB/s eta 0:00:04
         ------ --------------------------------- 0.3/1.5 MB 2.2 MB/s eta 0:00:01
         --------------------------- ------------ 1.0/1.5 MB 6.0 MB/s eta 0:00:01
         ---------------------------------------- 1.5/1.5 MB 7.4 MB/s eta 0:00:00
    Requirement already satisfied: click in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from nltk) (8.1.7)
    Requirement already satisfied: joblib in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from nltk) (1.3.2)
    Collecting regex>=2021.8.3 (from nltk)
      Downloading regex-2023.12.25-cp311-cp311-win_amd64.whl.metadata (41 kB)
         ---------------------------------------- 0.0/42.0 kB ? eta -:--:--
         ---------------------------------------- 42.0/42.0 kB ? eta 0:00:00
    Requirement already satisfied: tqdm in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from nltk) (4.66.1)
    Requirement already satisfied: colorama in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from click->nltk) (0.4.6)
    Downloading regex-2023.12.25-cp311-cp311-win_amd64.whl (269 kB)
       ---------------------------------------- 0.0/269.5 kB ? eta -:--:--
       --------------------------------------- 269.5/269.5 kB 16.2 MB/s eta 0:00:00
    Installing collected packages: regex, nltk
    Successfully installed nltk-3.8.1 regex-2023.12.25
    


```python
!pip install openpyxl

```

    Collecting openpyxl
      Downloading openpyxl-3.1.2-py2.py3-none-any.whl (249 kB)
         ---------------------------------------- 0.0/250.0 kB ? eta -:--:--
         - -------------------------------------- 10.2/250.0 kB ? eta -:--:--
         --------- --------------------------- 61.4/250.0 kB 544.7 kB/s eta 0:00:01
         -------------------------------------- 250.0/250.0 kB 1.7 MB/s eta 0:00:00
    Collecting et-xmlfile (from openpyxl)
      Downloading et_xmlfile-1.1.0-py3-none-any.whl (4.7 kB)
    Installing collected packages: et-xmlfile, openpyxl
    Successfully installed et-xmlfile-1.1.0 openpyxl-3.1.2
    


```python
import pandas as pd

# Make sure to replace 'Customer_Reviews.xlsx' with the correct path if your file is in a different directory
reviews_df = pd.read_excel('Customer_Reviews.xlsx')

```


```python
import pandas as pd

# Load the dataset from the Excel file
reviews_df = pd.read_excel('Customer_Reviews.xlsx')

# Display the first few rows to verify the data
reviews_df.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ReviewID</th>
      <th>ReviewText</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>This down give. American race investment evide...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Lot idea card benefit adult dream agency likel...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Send song western can smile thousand. None car...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Nearly human executive hour authority again bl...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Similar hotel risk common all natural dream. A...</td>
    </tr>
  </tbody>
</table>
</div>




```python
import nltk
from nltk.corpus import stopwords
from nltk.tokenize import RegexpTokenizer
from nltk.stem import WordNetLemmatizer

# Download necessary NLTK data
nltk.download('stopwords')
nltk.download('wordnet')

# Preprocessing function
def preprocess(text):
    # Tokenize and convert to lowercase
    tokenizer = RegexpTokenizer(r'\w+')
    tokens = tokenizer.tokenize(text.lower())
    
    # Remove stopwords
    stopped_tokens = [i for i in tokens if not i in stopwords.words('english')]
    
    # Lemmatize
    lemmatizer = WordNetLemmatizer()
    lemmatized_tokens = [lemmatizer.lemmatize(i) for i in stopped_tokens]
    
    return lemmatized_tokens

# Apply preprocessing to the review texts
reviews_df['processed_reviews'] = reviews_df['ReviewText'].apply(preprocess)
reviews_df['processed_reviews'].head()

```

    [nltk_data] Downloading package stopwords to
    [nltk_data]     C:\Users\Taraneh\AppData\Roaming\nltk_data...
    [nltk_data]   Package stopwords is already up-to-date!
    [nltk_data] Downloading package wordnet to
    [nltk_data]     C:\Users\Taraneh\AppData\Roaming\nltk_data...
    [nltk_data]   Package wordnet is already up-to-date!
    




    0    [give, american, race, investment, evidence, i...
    1    [lot, idea, card, benefit, adult, dream, agenc...
    2    [send, song, western, smile, thousand, none, c...
    3    [nearly, human, executive, hour, authority, bl...
    4    [similar, hotel, risk, common, natural, dream,...
    Name: processed_reviews, dtype: object




```python
!pip install gensim

```

    Collecting gensim
      Downloading gensim-4.3.2-cp311-cp311-win_amd64.whl.metadata (8.5 kB)
    Requirement already satisfied: numpy>=1.18.5 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from gensim) (1.26.0)
    Requirement already satisfied: scipy>=1.7.0 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from gensim) (1.11.2)
    Collecting smart-open>=1.8.1 (from gensim)
      Downloading smart_open-6.4.0-py3-none-any.whl.metadata (21 kB)
    Downloading gensim-4.3.2-cp311-cp311-win_amd64.whl (24.0 MB)
       ---------------------------------------- 0.0/24.0 MB ? eta -:--:--
       ---------------------------------------- 0.2/24.0 MB 5.9 MB/s eta 0:00:05
       - -------------------------------------- 1.0/24.0 MB 13.0 MB/s eta 0:00:02
       -- ------------------------------------- 1.4/24.0 MB 15.0 MB/s eta 0:00:02
       ---- ----------------------------------- 2.5/24.0 MB 14.5 MB/s eta 0:00:02
       ------ --------------------------------- 3.7/24.0 MB 17.0 MB/s eta 0:00:02
       -------- ------------------------------- 5.2/24.0 MB 19.7 MB/s eta 0:00:01
       ----------- ---------------------------- 6.7/24.0 MB 21.5 MB/s eta 0:00:01
       ------------- -------------------------- 8.3/24.0 MB 23.0 MB/s eta 0:00:01
       ---------------- ----------------------- 9.7/24.0 MB 24.0 MB/s eta 0:00:01
       ------------------- -------------------- 11.5/24.0 MB 27.3 MB/s eta 0:00:01
       --------------------- ------------------ 13.1/24.0 MB 31.1 MB/s eta 0:00:01
       ----------------------- ---------------- 14.4/24.0 MB 32.7 MB/s eta 0:00:01
       -------------------------- ------------- 16.0/24.0 MB 32.7 MB/s eta 0:00:01
       ----------------------------- ---------- 17.7/24.0 MB 31.2 MB/s eta 0:00:01
       -------------------------------- ------- 19.3/24.0 MB 34.6 MB/s eta 0:00:01
       ---------------------------------- ----- 20.8/24.0 MB 32.7 MB/s eta 0:00:01
       ------------------------------------ --- 22.2/24.0 MB 34.4 MB/s eta 0:00:01
       -------------------------------------- - 23.4/24.0 MB 31.2 MB/s eta 0:00:01
       ---------------------------------------  24.0/24.0 MB 31.2 MB/s eta 0:00:01
       ---------------------------------------- 24.0/24.0 MB 27.3 MB/s eta 0:00:00
    Downloading smart_open-6.4.0-py3-none-any.whl (57 kB)
       ---------------------------------------- 0.0/57.0 kB ? eta -:--:--
       ---------------------------------------- 57.0/57.0 kB ? eta 0:00:00
    Installing collected packages: smart-open, gensim
    Successfully installed gensim-4.3.2 smart-open-6.4.0
    


```python
from gensim import corpora

# Create a dictionary representation of the documents
dictionary = corpora.Dictionary(reviews_df['processed_reviews'])

# Filter out extremes to remove noise
dictionary.filter_extremes(no_below=5, no_above=0.5)

# Convert the dictionary to a bag of words corpus
corpus = [dictionary.doc2bow(text) for text in reviews_df['processed_reviews']]

```


```python
from gensim.models.ldamodel import LdaModel

# Set the number of topics
num_topics = 5

# Train the LDA model
lda_model = LdaModel(corpus=corpus, num_topics=num_topics, id2word=dictionary, passes=15, random_state=42)

# Print the topics
for idx, topic in lda_model.print_topics(-1):
    print('Topic: {} \nWords: {}'.format(idx, topic))
    print("\n")

```

    Topic: 0 
    Words: 0.064*"shoulder" + 0.064*"figure" + 0.052*"hour" + 0.040*"smile" + 0.039*"else" + 0.039*"six" + 0.035*"probably" + 0.031*"image" + 0.027*"animal" + 0.027*"require"
    
    
    Topic: 1 
    Words: 0.048*"laugh" + 0.048*"well" + 0.045*"despite" + 0.039*"writer" + 0.039*"scene" + 0.039*"begin" + 0.039*"give" + 0.039*"hospital" + 0.039*"opportunity" + 0.039*"country"
    
    
    Topic: 2 
    Words: 0.062*"final" + 0.061*"long" + 0.050*"believe" + 0.050*"low" + 0.049*"local" + 0.044*"worry" + 0.038*"decide" + 0.038*"perform" + 0.038*"tonight" + 0.038*"mind"
    
    
    Topic: 3 
    Words: 0.065*"mr" + 0.065*"consider" + 0.052*"ok" + 0.048*"image" + 0.040*"simple" + 0.040*"home" + 0.040*"food" + 0.040*"security" + 0.040*"candidate" + 0.027*"require"
    
    
    Topic: 4 
    Words: 0.068*"truth" + 0.054*"wait" + 0.054*"especially" + 0.046*"parent" + 0.046*"treat" + 0.035*"fish" + 0.035*"without" + 0.035*"world" + 0.034*"tend" + 0.034*"agree"
    
    
    


```python
!pip install pyldavis

```

    Collecting pyldavis
      Downloading pyLDAvis-3.4.1-py3-none-any.whl (2.6 MB)
         ---------------------------------------- 0.0/2.6 MB ? eta -:--:--
         ---------------------------------------- 0.0/2.6 MB ? eta -:--:--
         - -------------------------------------- 0.1/2.6 MB 1.2 MB/s eta 0:00:03
         --------- ------------------------------ 0.6/2.6 MB 4.3 MB/s eta 0:00:01
         ----------------- ---------------------- 1.1/2.6 MB 6.1 MB/s eta 0:00:01
         ---------------------------- ----------- 1.9/2.6 MB 8.0 MB/s eta 0:00:01
         ---------------------------------------  2.6/2.6 MB 9.7 MB/s eta 0:00:01
         ---------------------------------------- 2.6/2.6 MB 9.2 MB/s eta 0:00:00
    Requirement already satisfied: numpy>=1.24.2 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pyldavis) (1.26.0)
    Requirement already satisfied: scipy in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pyldavis) (1.11.2)
    Requirement already satisfied: pandas>=2.0.0 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pyldavis) (2.1.1)
    Requirement already satisfied: joblib>=1.2.0 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pyldavis) (1.3.2)
    Requirement already satisfied: jinja2 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pyldavis) (3.1.3)
    Collecting numexpr (from pyldavis)
      Downloading numexpr-2.9.0-cp311-cp311-win_amd64.whl.metadata (8.1 kB)
    Collecting funcy (from pyldavis)
      Downloading funcy-2.0-py2.py3-none-any.whl (30 kB)
    Collecting scikit-learn>=1.0.0 (from pyldavis)
      Downloading scikit_learn-1.4.0-1-cp311-cp311-win_amd64.whl.metadata (11 kB)
    Requirement already satisfied: gensim in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pyldavis) (4.3.2)
    Requirement already satisfied: setuptools in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pyldavis) (65.5.0)
    Requirement already satisfied: python-dateutil>=2.8.2 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pandas>=2.0.0->pyldavis) (2.8.2)
    Requirement already satisfied: pytz>=2020.1 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pandas>=2.0.0->pyldavis) (2023.3.post1)
    Requirement already satisfied: tzdata>=2022.1 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from pandas>=2.0.0->pyldavis) (2023.3)
    Collecting threadpoolctl>=2.0.0 (from scikit-learn>=1.0.0->pyldavis)
      Downloading threadpoolctl-3.2.0-py3-none-any.whl.metadata (10.0 kB)
    Requirement already satisfied: smart-open>=1.8.1 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from gensim->pyldavis) (6.4.0)
    Requirement already satisfied: MarkupSafe>=2.0 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from jinja2->pyldavis) (2.1.5)
    Requirement already satisfied: six>=1.5 in c:\users\taraneh\appdata\local\programs\python\python311\lib\site-packages (from python-dateutil>=2.8.2->pandas>=2.0.0->pyldavis) (1.16.0)
    Downloading scikit_learn-1.4.0-1-cp311-cp311-win_amd64.whl (10.6 MB)
       ---------------------------------------- 0.0/10.6 MB ? eta -:--:--
       -- ------------------------------------- 0.7/10.6 MB 15.8 MB/s eta 0:00:01
       ----- ---------------------------------- 1.4/10.6 MB 18.2 MB/s eta 0:00:01
       --------- ------------------------------ 2.5/10.6 MB 19.7 MB/s eta 0:00:01
       ------------ --------------------------- 3.3/10.6 MB 20.9 MB/s eta 0:00:01
       ----------------- ---------------------- 4.5/10.6 MB 22.2 MB/s eta 0:00:01
       ---------------------- ----------------- 5.9/10.6 MB 23.8 MB/s eta 0:00:01
       --------------------------- ------------ 7.3/10.6 MB 23.4 MB/s eta 0:00:01
       -------------------------------- ------- 8.5/10.6 MB 23.6 MB/s eta 0:00:01
       ------------------------------------ --- 9.7/10.6 MB 24.9 MB/s eta 0:00:01
       ---------------------------------------  10.6/10.6 MB 24.2 MB/s eta 0:00:01
       ---------------------------------------- 10.6/10.6 MB 23.4 MB/s eta 0:00:00
    Downloading numexpr-2.9.0-cp311-cp311-win_amd64.whl (96 kB)
       ---------------------------------------- 0.0/96.6 kB ? eta -:--:--
       ---------------------------------------- 96.6/96.6 kB 5.8 MB/s eta 0:00:00
    Downloading threadpoolctl-3.2.0-py3-none-any.whl (15 kB)
    Installing collected packages: funcy, threadpoolctl, numexpr, scikit-learn, pyldavis
    Successfully installed funcy-2.0 numexpr-2.9.0 pyldavis-3.4.1 scikit-learn-1.4.0 threadpoolctl-3.2.0
    


```python
import pyLDAvis.gensim_models as gensimvis
import pyLDAvis

# Prepare the visualization
pyLDAvis.enable_notebook()
vis = gensimvis.prepare(lda_model, corpus, dictionary)

# Display the visualization
vis

```





<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/bmabey/pyLDAvis@3.4.0/pyLDAvis/js/ldavis.v1.0.0.css">


<div id="ldavis_el3132418586215371041431969878" style="background-color:white;"></div>
<script type="text/javascript">

var ldavis_el3132418586215371041431969878_data = {"mdsDat": {"x": [0.12746934546890962, -0.07879110637060022, 0.11105387995316982, -0.03849547569676137, -0.12123664335471786], "y": [-0.14223099996232225, -0.034254159554558086, 0.13358914635949792, 0.07005152490830731, -0.02715551175092486], "topics": [1, 2, 3, 4, 5], "cluster": [1, 1, 1, 1, 1], "Freq": [24.004676124740897, 20.63105005851711, 18.795945989213184, 18.592838444571694, 17.975489382957118]}, "tinfo": {"Term": ["consider", "truth", "long", "mr", "shoulder", "figure", "final", "hour", "especially", "wait", "well", "believe", "image", "ok", "low", "laugh", "else", "treat", "six", "despite", "local", "parent", "country", "hospital", "mind", "opportunity", "candidate", "scene", "give", "food", "well", "laugh", "give", "opportunity", "begin", "scene", "despite", "analysis", "country", "writer", "hospital", "political", "data", "poor", "surface", "else", "responsibility", "matter", "idea", "pull", "mr", "security", "animal", "probably", "compare", "worry", "cultural", "simple", "decide", "home", "local", "without", "truth", "especially", "truth", "wait", "treat", "parent", "without", "tend", "agree", "fish", "world", "poor", "character", "affect", "learn", "measure", "month", "six", "hospital", "perform", "matter", "begin", "political", "home", "tonight", "decide", "candidate", "idea", "pull", "probably", "offer", "present", "smile", "security", "low", "writer", "image", "ok", "long", "final", "believe", "low", "local", "decide", "tonight", "step", "cultural", "worry", "perform", "mind", "responsibility", "affect", "compare", "country", "fish", "despite", "give", "political", "matter", "simple", "hotel", "star", "character", "offer", "without", "month", "smile", "measure", "require", "figure", "parent", "shoulder", "figure", "hour", "smile", "six", "probably", "else", "star", "pull", "offer", "present", "month", "measure", "animal", "require", "mind", "image", "surface", "tend", "agree", "hotel", "idea", "step", "scene", "food", "data", "responsibility", "compare", "believe", "candidate", "learn", "local", "world", "worry", "writer", "consider", "ok", "mr", "simple", "home", "food", "candidate", "image", "security", "character", "hotel", "present", "learn", "require", "world", "hour", "cultural", "wait", "opportunity", "analysis", "matter", "data", "surface", "idea", "step", "compare", "tonight", "star", "affect", "offer", "agree", "worry"], "Freq": [5.0, 6.0, 5.0, 7.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 6.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 4.3242553557461, 4.32575160460158, 3.4995663610106797, 3.4953277738034485, 3.4998706543172435, 3.502409233836091, 4.0480111673334696, 3.4630219117173024, 3.493160734730737, 3.5026879732296177, 3.499213985999322, 2.667581724103079, 2.66237629114665, 2.6635391623077007, 2.4815312485809193, 2.6632844637665714, 1.8329070334947446, 1.8299046168306983, 1.8360863101358658, 1.8332602490953471, 2.65888246601018, 1.824009228222259, 1.8341312676706552, 1.3254485181519198, 1.1320143067047408, 1.3849930022396038, 0.9974510151835065, 0.9965604949377227, 0.9950903043488271, 0.9948270317974023, 1.0897879784710658, 0.9965257786019186, 1.0300497385624894, 4.1553625316154115, 5.2719302418713285, 4.162565094269999, 3.559827868574324, 3.6002513989792164, 2.7434943762175767, 2.6295214224092653, 2.6257366381416065, 2.7493560669929593, 2.7354297832147862, 1.8839314923544002, 1.8839518655154959, 1.8817326358611106, 1.8801170875333757, 1.885600935640211, 1.8798672634515714, 1.8840979454152669, 1.8813303742973495, 1.8095958961174954, 1.027063428640264, 1.0244243095806023, 1.0248628382609237, 1.0233637492795937, 1.0244059592865657, 1.0218372793477133, 1.0248897857399617, 1.0180502554772393, 1.0219479590739493, 1.0241779532708992, 1.0222198902029, 1.020853949221213, 1.0225597318688362, 1.029727111085644, 1.0262296461856362, 1.024942813755012, 1.0256172954287324, 1.0236879137258217, 4.335195190268033, 4.365498846300319, 3.5188691634083633, 3.516208227442713, 3.4303590140579963, 2.6944368519556017, 2.691789606369907, 2.685603924118699, 2.5388417346092433, 3.137399099935726, 2.693565669892642, 2.6883859672916515, 1.848498664889686, 1.8487462764733105, 1.7181047726384118, 1.8486241161598582, 1.8249754328070753, 1.291318498405743, 1.0045682246996037, 1.0066837833175897, 1.0069422550583909, 0.9990715371473278, 1.002474781310777, 1.0045253764431072, 1.0031232314229168, 1.0064587476970654, 1.0005096852340367, 1.005270317406282, 1.0033777540156539, 1.0005942628217448, 1.006842999803711, 1.0050275106194688, 1.0047839140030428, 4.478249871206327, 4.468080538416535, 3.6068494116697662, 2.7615199774760573, 2.751544405790435, 2.4180104476904623, 2.7532077823661467, 1.901716406498783, 1.8972411500282909, 1.8986677942872152, 1.896268177601978, 1.896265443070266, 1.8951623850639363, 1.9040454462226895, 1.9019635560792354, 1.894726552795351, 2.155300860933038, 1.2236735123803528, 1.1425174291506344, 1.1437203626723527, 1.0366625346343392, 1.0363390134896424, 1.0342136963782849, 1.0289617677936675, 1.032633723019791, 1.0297190377542167, 1.0301454293776053, 1.0311055104401328, 1.0273855055853545, 1.0299557049631063, 1.0323956885450454, 1.0362243584814292, 1.03433108591821, 1.033023914651944, 1.0301731002342156, 4.364901363817604, 3.5288504996868535, 4.371850107667417, 2.697099104719789, 2.6939495345763977, 2.6905997958932355, 2.6903120064077535, 3.2708141163131303, 2.690375204273769, 1.848443161838651, 1.839835411059842, 1.849311691873796, 1.847059481070963, 1.8560436494182722, 1.8467598577221234, 1.8513855134811221, 1.1560700023593158, 1.2845724138528176, 1.007122388802815, 1.0060027668478124, 1.0086172323507654, 1.0066348714001334, 1.0066511744352908, 1.0085480546069892, 1.0055826017525382, 1.0036258598571537, 1.002849168155193, 1.0068344104790876, 1.004763106715029, 1.006786760295249, 1.008340836106069, 1.0060081802108376], "Total": [5.0, 6.0, 5.0, 7.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 6.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.0, 5.011013937243265, 5.866111360147834, 5.016966907211884, 5.017186121128763, 5.0330832175234, 5.038248649956628, 5.852126628551162, 5.017422332255688, 5.85622917382477, 5.893597979571913, 5.888460206151877, 5.039186010720742, 5.044656805098202, 5.0554639806885735, 5.050834192063355, 5.926621257170834, 5.050562898193873, 5.045636623434241, 5.066914357734814, 5.088235580984756, 7.54186460225602, 5.88540488799861, 5.927546587683008, 5.104986058306107, 5.055962462325368, 6.7325393162688805, 5.0356184935190935, 5.0360440979903744, 5.051443318008698, 5.052169669980243, 5.895381153133522, 5.083994374853369, 6.809927185632517, 5.116881015573728, 6.809927185632517, 5.956413982776516, 5.099493987121042, 5.945712186530728, 5.083994374853369, 5.105998342964188, 5.112295855179844, 5.929439341034189, 5.95106692630405, 5.0554639806885735, 5.074309026791601, 5.074035155247444, 5.0956457201181715, 5.1167856844999875, 5.116704167344989, 5.13809581144436, 5.888460206151877, 5.905568882110904, 5.045636623434241, 5.0330832175234, 5.039186010720742, 5.052169669980243, 5.057827980353254, 5.051443318008698, 5.079663232671956, 5.066914357734814, 5.088235580984756, 5.104986058306107, 5.100770364473018, 5.1009309184509135, 5.12204340103618, 5.88540488799861, 5.918089394984525, 5.893597979571913, 6.78625091204477, 5.919009973212761, 5.041282654320837, 5.902025236054129, 5.062700953914263, 5.918089394984525, 5.895381153133522, 5.051443318008698, 5.057827980353254, 5.063166040824562, 5.0356184935190935, 6.7325393162688805, 5.905568882110904, 5.917456465764342, 5.050562898193873, 5.074035155247444, 5.055962462325368, 5.85622917382477, 5.929439341034189, 5.852126628551162, 5.016966907211884, 5.039186010720742, 5.045636623434241, 5.0360440979903744, 5.057533262628087, 5.0786571370030815, 5.074309026791601, 5.100770364473018, 5.083994374853369, 5.116704167344989, 5.12204340103618, 5.1167856844999875, 5.940019922617607, 5.987694419697903, 5.945712186530728, 5.988128430173054, 5.987694419697903, 5.966722915808693, 5.12204340103618, 5.13809581144436, 5.104986058306107, 5.926621257170834, 5.0786571370030815, 5.088235580984756, 5.100770364473018, 5.1009309184509135, 5.116704167344989, 5.1167856844999875, 5.927546587683008, 5.940019922617607, 5.917456465764342, 6.78625091204477, 5.050834192063355, 5.105998342964188, 5.112295855179844, 5.057533262628087, 5.066914357734814, 5.063166040824562, 5.038248649956628, 5.057486526883604, 5.044656805098202, 5.050562898193873, 5.055962462325368, 5.062700953914263, 5.079663232671956, 5.0956457201181715, 5.895381153133522, 5.95106692630405, 6.7325393162688805, 5.893597979571913, 5.042648308044017, 5.919009973212761, 7.54186460225602, 5.0360440979903744, 5.052169669980243, 5.057486526883604, 5.079663232671956, 6.78625091204477, 5.88540488799861, 5.074309026791601, 5.057533262628087, 5.1009309184509135, 5.0956457201181715, 5.940019922617607, 5.95106692630405, 5.966722915808693, 5.0356184935190935, 5.956413982776516, 5.017186121128763, 5.017422332255688, 5.045636623434241, 5.044656805098202, 5.050834192063355, 5.066914357734814, 5.063166040824562, 5.055962462325368, 5.057827980353254, 5.0786571370030815, 5.074035155247444, 5.100770364473018, 5.112295855179844, 6.7325393162688805], "Category": ["Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Default", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic1", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic2", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic3", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic4", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5", "Topic5"], "logprob": [30.0, 29.0, 28.0, 27.0, 26.0, 25.0, 24.0, 23.0, 22.0, 21.0, 20.0, 19.0, 18.0, 17.0, 16.0, 15.0, 14.0, 13.0, 12.0, 11.0, 10.0, 9.0, 8.0, 7.0, 6.0, 5.0, 4.0, 3.0, 2.0, 1.0, -3.0384, -3.0381, -3.25, -3.2512, -3.2499, -3.2492, -3.1044, -3.2605, -3.2519, -3.2491, -3.2501, -3.5215, -3.5234, -3.523, -3.5938, -3.5231, -3.8968, -3.8984, -3.895, -3.8966, -3.5248, -3.9016, -3.8961, -4.2209, -4.3787, -4.177, -4.5052, -4.5061, -4.5076, -4.5079, -4.4167, -4.5061, -4.4731, -2.9268, -2.6888, -2.9251, -3.0815, -3.0702, -3.342, -3.3844, -3.3859, -3.3398, -3.3449, -3.7179, -3.7178, -3.719, -3.7199, -3.717, -3.72, -3.7178, -3.7192, -3.7581, -4.3245, -4.3271, -4.3267, -4.3281, -4.3271, -4.3296, -4.3266, -4.3333, -4.3295, -4.3273, -4.3292, -4.3306, -4.3289, -4.3219, -4.3253, -4.3266, -4.3259, -4.3278, -2.7913, -2.7843, -2.9999, -3.0007, -3.0254, -3.2669, -3.2679, -3.2702, -3.3264, -3.1147, -3.2672, -3.2691, -3.6437, -3.6436, -3.7168, -3.6436, -3.6565, -4.0024, -4.2535, -4.2514, -4.2511, -4.259, -4.2556, -4.2535, -4.2549, -4.2516, -4.2576, -4.2528, -4.2547, -4.2575, -4.2512, -4.253, -4.2533, -2.748, -2.7502, -2.9644, -3.2314, -3.235, -3.3643, -3.2344, -3.6044, -3.6068, -3.606, -3.6073, -3.6073, -3.6079, -3.6032, -3.6043, -3.6081, -3.4793, -4.0453, -4.114, -4.1129, -4.2112, -4.2115, -4.2136, -4.2186, -4.2151, -4.2179, -4.2175, -4.2166, -4.2202, -4.2177, -4.2153, -4.2116, -4.2134, -4.2147, -4.2175, -2.7398, -2.9525, -2.7382, -3.2213, -3.2224, -3.2237, -3.2238, -3.0284, -3.2237, -3.5991, -3.6038, -3.5986, -3.5998, -3.595, -3.6, -3.5975, -4.0684, -3.963, -4.2063, -4.2074, -4.2048, -4.2068, -4.2068, -4.2049, -4.2079, -4.2098, -4.2106, -4.2066, -4.2087, -4.2067, -4.2051, -4.2074], "loglift": [30.0, 29.0, 28.0, 27.0, 26.0, 25.0, 24.0, 23.0, 22.0, 21.0, 20.0, 19.0, 18.0, 17.0, 16.0, 15.0, 14.0, 13.0, 12.0, 11.0, 10.0, 9.0, 8.0, 7.0, 6.0, 5.0, 4.0, 3.0, 2.0, 1.0, 1.2795, 1.1223, 1.0667, 1.0655, 1.0636, 1.0633, 1.0583, 1.0561, 0.9102, 0.9066, 0.9065, 0.7908, 0.7878, 0.7861, 0.7162, 0.627, 0.4133, 0.4127, 0.4118, 0.4061, 0.3844, 0.2555, 0.2539, 0.0785, -0.0696, -0.1543, -0.1922, -0.1931, -0.1977, -0.1981, -0.2613, -0.2027, -0.4619, 1.3702, 1.3224, 1.22, 1.2189, 1.0767, 0.9615, 0.9148, 0.9121, 0.8098, 0.8011, 0.5913, 0.5876, 0.5864, 0.5813, 0.5801, 0.5771, 0.5751, 0.4374, 0.3956, -0.0134, -0.0135, -0.0143, -0.0183, -0.0185, -0.0197, -0.0223, -0.0265, -0.0268, -0.028, -0.029, -0.0304, -0.0329, -0.1648, -0.1737, -0.1709, -0.3112, -0.1764, 1.5206, 1.37, 1.3078, 1.1509, 1.13, 1.043, 1.0408, 1.0374, 0.9867, 0.908, 0.8865, 0.8826, 0.6664, 0.6619, 0.5922, 0.5185, 0.4932, 0.1604, 0.0633, 0.0609, 0.0599, 0.054, 0.0531, 0.051, 0.0505, 0.0486, 0.0459, 0.0443, 0.0413, 0.0396, -0.1034, -0.1132, -0.1064, 1.3918, 1.3896, 1.179, 1.0646, 1.0579, 0.9351, 0.9157, 0.7001, 0.6959, 0.6942, 0.6929, 0.6898, 0.6892, 0.5468, 0.5436, 0.5436, 0.5354, 0.2647, 0.1852, 0.185, 0.0975, 0.0954, 0.094, 0.0939, 0.0936, 0.0934, 0.0926, 0.0925, 0.0875, 0.0867, 0.0859, -0.0562, -0.0674, -0.1921, -0.0617, 1.5718, 1.199, 1.1709, 1.0917, 1.0874, 1.0851, 1.0806, 0.9863, 0.9334, 0.7063, 0.705, 0.7016, 0.7014, 0.5529, 0.546, 0.5459, 0.2447, 0.1821, 0.1104, 0.1092, 0.1062, 0.1044, 0.1032, 0.1019, 0.0997, 0.0992, 0.0981, 0.0979, 0.0968, 0.0935, 0.0928, -0.1848]}, "token.table": {"Topic": [2, 3, 5, 2, 4, 5, 1, 5, 1, 2, 3, 4, 1, 2, 3, 4, 2, 4, 5, 2, 3, 5, 1, 3, 4, 5, 5, 1, 3, 1, 3, 5, 1, 4, 5, 1, 2, 3, 1, 3, 1, 4, 2, 3, 4, 3, 4, 2, 3, 5, 1, 4, 5, 1, 3, 1, 2, 5, 1, 2, 1, 3, 4, 5, 4, 5, 1, 2, 4, 5, 2, 4, 5, 1, 2, 2, 4, 5, 1, 3, 4, 3, 2, 3, 4, 1, 2, 3, 5, 2, 3, 4, 1, 3, 4, 2, 3, 4, 1, 5, 2, 3, 4, 5, 2, 4, 5, 1, 5, 2, 3, 5, 1, 2, 3, 1, 2, 3, 1, 2, 2, 4, 5, 1, 2, 4, 1, 2, 4, 2, 3, 4, 5, 1, 3, 4, 1, 4, 1, 2, 5, 4, 5, 1, 3, 5, 2, 4, 2, 3, 4, 1, 3, 4, 5, 3, 4, 5, 1, 4, 5, 1, 2, 4, 2, 3, 5, 1, 2, 1, 2, 2, 5, 1, 1, 2, 3, 2, 4, 5, 1, 3, 4, 5, 1, 2, 4], "Freq": [0.3941636072291791, 0.3941636072291791, 0.19708180361458955, 0.5868204980665118, 0.19560683268883727, 0.19560683268883727, 0.5979165797373264, 0.1993055265791088, 0.3374077234847632, 0.1687038617423816, 0.1687038617423816, 0.3374077234847632, 0.5960561092165276, 0.19868536973884254, 0.790092094400198, 0.1975230236000495, 0.19686344432601086, 0.19686344432601086, 0.5905903329780325, 0.3941423333581569, 0.19707116667907845, 0.3941423333581569, 0.19778627856743897, 0.39557255713487793, 0.19778627856743897, 0.19778627856743897, 0.7932339825522261, 0.5122750341480687, 0.34151668943204583, 0.1985853378859048, 0.5957560136577144, 0.1985853378859048, 0.5946886212295269, 0.1982295404098423, 0.1982295404098423, 0.19796322299310773, 0.19796322299310773, 0.5938896689793232, 0.6835122091317936, 0.1708780522829484, 0.506190605038274, 0.506190605038274, 0.7817262093501116, 0.16700919083483437, 0.6680367633393375, 0.677733462670561, 0.16943336566764025, 0.5059500278953444, 0.33730001859689623, 0.16865000929844812, 0.197726676024621, 0.197726676024621, 0.5931800280738629, 0.5979708567914815, 0.19932361893049386, 0.19793476176026975, 0.19793476176026975, 0.5938042852808092, 0.5094710493017847, 0.3396473662011898, 0.19772484886839123, 0.19772484886839123, 0.19772484886839123, 0.39544969773678246, 0.6703847415810266, 0.3351923707905133, 0.3947175457873949, 0.19735877289369744, 0.19735877289369744, 0.19735877289369744, 0.14735676781787152, 0.29471353563574304, 0.44207030345361453, 0.6818827251003967, 0.17047068127509918, 0.39249196467952613, 0.19624598233976306, 0.39249196467952613, 0.1696243167362433, 0.50887295020873, 0.1696243167362433, 0.793448864957341, 0.16897345296059266, 0.6758938118423706, 0.16897345296059266, 0.3963820919467499, 0.19819104597337495, 0.19819104597337495, 0.19819104597337495, 0.3908703868638657, 0.19543519343193286, 0.3908703868638657, 0.16899152630619863, 0.5069745789185959, 0.33798305261239725, 0.3908766140446579, 0.19543830702232895, 0.3908766140446579, 0.39777961528275135, 0.5303728203770018, 0.19604881783446337, 0.19604881783446337, 0.39209763566892675, 0.19604881783446337, 0.16894717267340795, 0.16894717267340795, 0.6757886906936318, 0.5979447298887652, 0.19931490996292175, 0.6727537214232304, 0.1681884303558076, 0.1681884303558076, 0.16933169690547356, 0.3386633938109471, 0.5079950907164207, 0.5953342451772122, 0.19844474839240409, 0.19844474839240409, 0.5934173423962144, 0.39561156159747624, 0.19604264711424224, 0.3920852942284845, 0.3920852942284845, 0.19588692086101633, 0.19588692086101633, 0.39177384172203267, 0.39306356165469214, 0.19653178082734607, 0.39306356165469214, 0.16834960370963317, 0.16834960370963317, 0.33669920741926634, 0.33669920741926634, 0.39599546433036564, 0.39599546433036564, 0.19799773216518282, 0.7939266753010362, 0.19848166882525906, 0.339823688949312, 0.169911844474656, 0.5097355334239679, 0.6679883450469685, 0.16699708626174212, 0.19856855510837335, 0.19856855510837335, 0.59570566532512, 0.38924926147645816, 0.5838738922146872, 0.1952345815339444, 0.1952345815339444, 0.5857037446018333, 0.1969024435049972, 0.1969024435049972, 0.3938048870099944, 0.1969024435049972, 0.5925146392219511, 0.19750487974065037, 0.19750487974065037, 0.3959741943504514, 0.1979870971752257, 0.1979870971752257, 0.19584808549300653, 0.5875442564790195, 0.19584808549300653, 0.19771332751616374, 0.5931399825484912, 0.19771332751616374, 0.1960978878542727, 0.7843915514170908, 0.1468444482210889, 0.7342222411054447, 0.6715449952884982, 0.16788624882212455, 0.7982416433270869, 0.19669573297449638, 0.5900871989234892, 0.19669573297449638, 0.5041112857830302, 0.16803709526101004, 0.3360741905220201, 0.14853236691593388, 0.4455971007478017, 0.14853236691593388, 0.14853236691593388, 0.6787025538329209, 0.16967563845823022, 0.16967563845823022], "Term": ["affect", "affect", "affect", "agree", "agree", "agree", "analysis", "analysis", "animal", "animal", "animal", "animal", "begin", "begin", "believe", "believe", "candidate", "candidate", "candidate", "character", "character", "character", "compare", "compare", "compare", "compare", "consider", "country", "country", "cultural", "cultural", "cultural", "data", "data", "data", "decide", "decide", "decide", "despite", "despite", "else", "else", "especially", "figure", "figure", "final", "final", "fish", "fish", "fish", "food", "food", "food", "give", "give", "home", "home", "home", "hospital", "hospital", "hotel", "hotel", "hotel", "hotel", "hour", "hour", "idea", "idea", "idea", "idea", "image", "image", "image", "laugh", "laugh", "learn", "learn", "learn", "local", "local", "local", "long", "low", "low", "low", "matter", "matter", "matter", "matter", "measure", "measure", "measure", "mind", "mind", "mind", "month", "month", "month", "mr", "mr", "offer", "offer", "offer", "offer", "ok", "ok", "ok", "opportunity", "opportunity", "parent", "parent", "parent", "perform", "perform", "perform", "political", "political", "political", "poor", "poor", "present", "present", "present", "probably", "probably", "probably", "pull", "pull", "pull", "require", "require", "require", "require", "responsibility", "responsibility", "responsibility", "scene", "scene", "security", "security", "security", "shoulder", "shoulder", "simple", "simple", "simple", "six", "six", "smile", "smile", "smile", "star", "star", "star", "star", "step", "step", "step", "surface", "surface", "surface", "tend", "tend", "tend", "tonight", "tonight", "tonight", "treat", "treat", "truth", "truth", "wait", "wait", "well", "without", "without", "without", "world", "world", "world", "worry", "worry", "worry", "worry", "writer", "writer", "writer"]}, "R": 30, "lambda.step": 0.01, "plot.opts": {"xlab": "PC1", "ylab": "PC2"}, "topic.order": [2, 5, 3, 1, 4]};

function LDAvis_load_lib(url, callback){
  var s = document.createElement('script');
  s.src = url;
  s.async = true;
  s.onreadystatechange = s.onload = callback;
  s.onerror = function(){console.warn("failed to load library " + url);};
  document.getElementsByTagName("head")[0].appendChild(s);
}

if(typeof(LDAvis) !== "undefined"){
   // already loaded: just create the visualization
   !function(LDAvis){
       new LDAvis("#" + "ldavis_el3132418586215371041431969878", ldavis_el3132418586215371041431969878_data);
   }(LDAvis);
}else if(typeof define === "function" && define.amd){
   // require.js is available: use it to load d3/LDAvis
   require.config({paths: {d3: "https://d3js.org/d3.v5"}});
   require(["d3"], function(d3){
      window.d3 = d3;
      LDAvis_load_lib("https://cdn.jsdelivr.net/gh/bmabey/pyLDAvis@3.4.0/pyLDAvis/js/ldavis.v3.0.0.js", function(){
        new LDAvis("#" + "ldavis_el3132418586215371041431969878", ldavis_el3132418586215371041431969878_data);
      });
    });
}else{
    // require.js not available: dynamically load d3 & LDAvis
    LDAvis_load_lib("https://d3js.org/d3.v5.js", function(){
         LDAvis_load_lib("https://cdn.jsdelivr.net/gh/bmabey/pyLDAvis@3.4.0/pyLDAvis/js/ldavis.v3.0.0.js", function(){
                 new LDAvis("#" + "ldavis_el3132418586215371041431969878", ldavis_el3132418586215371041431969878_data);
            })
         });
}
</script>




```python

```
