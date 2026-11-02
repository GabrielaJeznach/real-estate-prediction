{\rtf1\ansi\ansicpg1252\cocoartf2822
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\paperw11900\paperh16840\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 # \uc0\u55356 \u57305 \u65039  Predykcja cen mieszka\u324  w Poznaniu z wykorzystaniem Ensemble Learning i NLP\
\
Kompleksowy projekt z zakresu Data Science i Machine Learning, skupiaj\uc0\u261 cy si\u281  na predykcji cen za metr kwadratowy nieruchomo\u347 ci (`price_per_m`) w Poznaniu. Projekt \u322 \u261 czy in\u380 ynieri\u281  cech geoprzestrzennych, zaawansowane przetwarzanie j\u281 zyka naturalnego (NLP) oraz zaawansowane metody zespo\u322 owe (Bagging, Boosting, Stacking).\
\
---\
\
## \uc0\u55357 \u56523  Spis tre\u347 ci\
- [O projekcie](#-o-projekcie)\
- [Metodologia i Architektura Danych](#-metodologia-i-architektura-danych)\
- [Przetwarzanie J\uc0\u281 zyka Naturalnego (NLP)](#-przetwarzanie-j\u281 zyka-naturalnego-nlp)\
- [Modelowanie i Ensemble Learning](#-modelowanie-i-ensemble-learning)\
- [Wyniki i Por\'f3wnanie](#-wyniki-i-por\'f3wnanie)\
- [Wymagania i Uruchomienie](#-wymagania-i-uruchomienie)\
\
---\
\
## \uc0\u55356 \u57263  O projekcie\
G\uc0\u322 \'f3wnym celem projektu jest oszacowanie rynkowej ceny nieruchomo\u347 ci na podstawie bogatego zestawu danych og\u322 oszeniowych. \
* **Czasowy podzia\uc0\u322  danych (*Time-based split*):** Aby symulowa\u263  rzeczywiste warunki rynkowe i unika\u263  *data leakage*, model testowano na najnowszych danych z ostatnich 6 miesi\u281 cy.\
* **Geoprzestrze\uc0\u324 :** Wykorzystano wsp\'f3\u322 rz\u281 dne geograficzne do wyliczenia odleg\u322 o\u347 ci mieszka\u324  od \u347 cis\u322 ego centrum oraz stacji kolejowej za pomoc\u261  wzoru Haversine'a.\
\
---\
\
## \uc0\u55357 \u56612  Przetwarzanie J\u281 zyka Naturalnego (NLP)\
Opisy i tytu\uc0\u322 y ofert og\u322 oszeniowych zosta\u322 y poddane czyszczeniu, a nast\u281 pnie przekszta\u322 cone numerycznie przy u\u380 yciu trzech r\'f3\u380 nych podej\u347 \u263 :\
1. **TF-IDF + TruncatedSVD (LSA):** Ekstrakcja najwa\uc0\u380 niejszych n-gram\'f3w z redukcj\u261  wymiarowo\u347 ci.\
2. **FastText:** Wektory osadzone (*embeddings*) dla j\uc0\u281 zyka polskiego.\
3. **OpenAI Embeddings:** Semantyczna reprezentacja tekstu generowana przez modele LLM.\
\
---\
\
## Modelowanie i Ensemble Learning\
W duchu nowoczesnego podej\uc0\u347 cia do uczenia maszynowego (wzorowanego na zaawansowanych studiach nad modelami zespo\u322 owymi), przetestowano i zoptymalizowano nast\u281 puj\u261 ce podej\u347 cia:\
- **Bagging:** Modele r\'f3wnoleg\uc0\u322 e redukuj\u261 ce wariancj\u281  (Random Forest).\
- **Boosting:** Modele sekwencyjne redukuj\uc0\u261 ce b\u322 \u261 d/obci\u261 \u380 enie (XGBoost, LightGBM).\
- **Stacking / Blending:** \uc0\u321 \u261 czenie prognoz r\'f3\u380 nych modeli bazowych przy u\u380 yciu meta-modelu w celu wyci\u261 gni\u281 cia maksymalnej precyzji z danych.\
\
---\
\
## Wyniki i Por\'f3wnanie\
Dodanie cech tekstowych (NLP) oraz optymalizacja modeli przynios\uc0\u322 y dramatyczny wzrost skuteczno\u347 ci predykcji w stosunku do bazy numerycznej (*baseline*).\
\
| Model i Podej\uc0\u347 cie | Wsp\'f3\u322 czynnik $R^2$ | MAE (PLN) | RMSE (PLN) | MAPE (%) |\
| :--- | :---: | :---: | :---: | :---: |\
| **XGBoost (Baseline - bez tekstu)** | 0.2754 | 461.53 | 752.36 | 5.70% |\
| **XGBoost (OpenAI features)** | 0.4202 | 421.58 | 673.02 | 5.20% |\
| **XGBoost (TF-IDF + LSA)** | **0.4837** | **388.89** | **635.12** | **4.76%** |\
\
*Szczeg\'f3\uc0\u322 owe wyniki dla poszczeg\'f3lnych wariant\'f3w znajduj\u261  si\u281  w folderze `results/`.*\
\
---\
\
## Wymagania i Uruchomienie\
Sklonuj repozytorium i zainstaluj wymagane pakiety\
\
```bash\
pip install -r requirements.txt}