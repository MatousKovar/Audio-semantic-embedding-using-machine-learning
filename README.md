# MVI - Semestrální práce

## Úvod
Tato semestrální práce se zabývá datasetem z webu [Kaggle](https://www.kaggle.com/datasets/andradaolteanu/gtzan-dataset-music-genre-classification). Cílem je objevit skrytou strukturu v úryvcích písní a reprezentovat je tak, aby výsledná reprezentace nesla sémantický význam. Získání takovéto reprezentace, může být výhodné pro tvorbu například doporučovacích systémů.

## Použité technologie
Celá práce je vypracována v prostředí Google Colab. Implementace v jazyce Python využívá knihovny [PyTorch](https://pytorch.org/), [Librosa](https://librosa.org/doc/latest/index.html), [Matplotlib](https://matplotlib.org/) a [umap-learn](https://pypi.org/project/umap-learn/).

## O datasetu
Dataset obsahuje celkem 1000 třicetisekundových úryvků písní, které jsou roztříděny do 10 kategorií. Pro jednodušší práci s Colab notebookem jsem dataset uložil na Google Drive odkaz je v souboru spectrograms.txt. V tomto repozitáři není dataset kvůli své velikosti přiložen, je však možné jej stáhnout [zde](https://www.kaggle.com/datasets/andradaolteanu/gtzan-dataset-music-genre-classification).

## O implementaci - 1. milestone
Data jsou nejprve pomocí knihovny Librosa převedena na spektrogramy, čímž je získána 2D reprezentace písní. Následuje aplikace jednotlivých modelů.

V této práci jsou porovnány celkem tři přístupy:

1.  **Konvoluční autoenkodér:** Klasický přístup, který se učí komprimovat vstup do nízkodimenzionální reprezentace a následně jej rekonstruovat s co nejmenší chybou.
2.  **Autoenkodér s Triplet Loss:** Tento přístup využívá odlišnou ztrátovou funkci (Triplet Loss). Ta pracuje s labely jednotlivých datových bodů a snaží se formovat latentní prostor tak, aby se zástupci stejných kategorií shlukovali k sobě.
3.  **Hybridní CRNN enkodér:** Třetí přístup rozšiřuje předchozí model o rekurentní neuronovou síť. Po aplikaci konvolučních vrstev je výsledek zpracován pomocí RNN, což umožňuje sekvenční průchod vstupem se zachováním kontextu (paměti).

## Evaluace - 1. milestone
Kvalita embeddingů je kvantitativně vyhodnocena pomocí algoritmu KNN. Cílem je dosáhnout co nejvyšší klasifikační přesnosti na validační množině přímo v prostoru embeddingů.

Druhou validační metodou je projekce dat do 2D pomocí metody UMAP a následné vizuální zhodnocení vzniklých shluků.

## Aktuální stav práce - 1.milestone
V praktické části zbývá pouze finalizace kódu a spuštění evaluační - poslední části. V notebooku v tomto repozitáři, jsou i podrobnější popisy metodiky než v tomto readme.

Nejlepším modelem podle výpisů při trénování mi vyšel model používající RNN, dosáhl přesnosti přes 70 procent.

## Rešerše - 1.milestone
V rámci práce jsem použil hlavně metody které se používají pro zpracování obrazu. [Zde](https://ietresearch.onlinelibrary.wiley.com/doi/full/10.1049/iet-spr.2019.0381) je využítí CNN s předzpracováním převodem na spektrogram.

Druhý článek, který dává dobrý úvod do zpracování zvuku je [tento](https://arxiv.org/pdf/1905.00078). 

Pro RNN jsem využil [GRU](https://arxiv.org/pdf/1406.1078), místo klasické LSTM.

## Dosažení dat
- Dataset je dostupný na [Kaggle](https://www.kaggle.com/datasets/andradaolteanu/)
- Jinak je možné stáhnout rovnou spektrogramy, dostupné naodkazu v spectrograms.txt
- Modely je možné stáhnout z odkazu v models.txt
- Google colab notebook je stažený a pojmenovaný jako mvi.ipynb