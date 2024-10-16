{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "prostate-aluminum",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "importing Jupyter notebook from week1_data_analysis.ipynb\n"
     ]
    }
   ],
   "source": [
    "import pandas as pd\n",
    "import matplotlib.pyplot as plt\n",
    "from pandasql import sqldf\n",
    "pysqldf = lambda q: sqldf(q, globals())\n",
    "\n",
    "import import_ipynb\n",
    "from week1_data_analysis import summer_events, winter_events"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "sized-break",
   "metadata": {},
   "source": [
    "## Beyond Descriptive Stats"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "motivated-change",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Summer Olympics:\n",
    "summer_medal_count = pysqldf('''\n",
    "                         SELECT\n",
    "                             Year,\n",
    "                             COUNT(*) AS total_count,\n",
    "                             SUM(CASE\n",
    "                                   WHEN Medal IS NOT NULL THEN 1 ELSE 0\n",
    "                                 END) AS medal_count,\n",
    "                             SUM(CASE\n",
    "                                   WHEN Medal = \"Gold\" THEN 1 ELSE 0\n",
    "                                 END) AS gold_count,\n",
    "                             SUM(CASE\n",
    "                                   WHEN Medal = \"Silver\" THEN 1 ELSE 0\n",
    "                                 END) AS silver_count,\n",
    "                             SUM(CASE\n",
    "                                   WHEN Medal = \"Bronze\" THEN 1 ELSE 0\n",
    "                                 END) AS bronze_count\n",
    "                             FROM\n",
    "                               summer_events\n",
    "                             GROUP BY\n",
    "                               Year \n",
    "                                   ''')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "incredible-trunk",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Winter Olympics:\n",
    "winter_medal_count = pysqldf('''\n",
    "                         SELECT\n",
    "                             Year,\n",
    "                             COUNT(*) AS total_count,\n",
    "                             SUM(CASE\n",
    "                                   WHEN Medal IS NOT NULL THEN 1 ELSE 0\n",
    "                                 END) AS medal_count,\n",
    "                             SUM(CASE\n",
    "                                   WHEN Medal = \"Gold\" THEN 1 ELSE 0\n",
    "                                 END) AS gold_count,\n",
    "                             SUM(CASE\n",
    "                                   WHEN Medal = \"Silver\" THEN 1 ELSE 0\n",
    "                                 END) AS silver_count,\n",
    "                             SUM(CASE\n",
    "                                   WHEN Medal = \"Bronze\" THEN 1 ELSE 0\n",
    "                                 END) AS bronze_count\n",
    "                             FROM\n",
    "                               winter_events\n",
    "                             GROUP BY\n",
    "                               Year \n",
    "                                   ''')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "enabling-comparison",
   "metadata": {},
   "source": [
    "I just created two tables to count the total number of medals in the winter and summer olympics. I will calculate the Pearon correlation coefficient between the total number of medals in the winter and summer olympics."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "behavioral-header",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "   Year  total_count  medal_count  gold_count  silver_count  bronze_count\n",
      "0  1896          380          143          62            43            38\n",
      "1  1900         1936          604         201           228           175\n",
      "2  1904         1301          486         173           163           150\n",
      "3  1906         1733          458         157           156           145\n",
      "4  1908         3101          831         294           281           256\n"
     ]
    }
   ],
   "source": [
    "print(summer_medal_count.head())\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "medical-destiny",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "   Year  total_count  medal_count  gold_count  silver_count  bronze_count\n",
      "0  1924          460          130          55            38            37\n",
      "1  1928          582           89          30            28            31\n",
      "2  1932          352           92          32            32            28\n",
      "3  1936          895          108          36            37            35\n",
      "4  1948         1075          135          41            48            46\n"
     ]
    }
   ],
   "source": [
    "print(winter_medal_count.head())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "finnish-qatar",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "    Year  total_count  medal_count  gold_count  silver_count  bronze_count\n",
      "0   1896          380          143          62            43            38\n",
      "1   1900         1936          604         201           228           175\n",
      "2   1904         1301          486         173           163           150\n",
      "3   1906         1733          458         157           156           145\n",
      "4   1908         3101          831         294           281           256\n",
      "5   1912         4040          941         326           315           300\n",
      "6   1920         4292         1308         493           448           367\n",
      "7   1924         5233          832         277           281           274\n",
      "8   1928         4992          734         245           239           250\n",
      "9   1932         2969          647         229           214           204\n",
      "10  1936         6506          917         312           310           295\n",
      "11  1948         6405          852         289           284           279\n",
      "12  1952         8270          897         306           291           300\n",
      "13  1956         5127          893         302           293           298\n",
      "14  1960         8119          911         309           294           308\n",
      "15  1964         7702         1029         347           339           343\n",
      "16  1968         8588         1057         359           340           358\n",
      "17  1972        10304         1215         404           392           419\n",
      "18  1976         8641         1320         438           434           448\n",
      "19  1980         7191         1384         457           458           469\n",
      "20  1984         9454         1476         497           477           502\n",
      "21  1988        12037         1582         520           513           549\n",
      "22  1992        12977         1712         559           549           604\n",
      "23  1996        13780         1842         608           605           629\n",
      "24  2000        13821         2004         663           661           680\n",
      "25  2004        13443         2001         664           660           677\n",
      "26  2008        13602         2048         671           667           710\n",
      "27  2012        12920         1941         632           630           679\n",
      "28  2016        13688         2023         665           655           703\n"
     ]
    }
   ],
   "source": [
    "print(summer_medal_count)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "welsh-ethiopia",
   "metadata": {},
   "source": [
    "The length of the array of the number of medal count in the winter Olympics and summer Olympics are different because Winter olympics started in 1924, but Summer olympics started in 1896. Therefore I have to create a new shortened table of the summer olympics started in 1924 to match the length of the winter olympics."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "modified-serve",
   "metadata": {},
   "outputs": [],
   "source": [
    "summer_medal_count_new = summer_medal_count[7:]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "fossil-gravity",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "    Year  total_count  medal_count  gold_count  silver_count  bronze_count\n",
      "7   1924         5233          832         277           281           274\n",
      "8   1928         4992          734         245           239           250\n",
      "9   1932         2969          647         229           214           204\n",
      "10  1936         6506          917         312           310           295\n",
      "11  1948         6405          852         289           284           279\n",
      "12  1952         8270          897         306           291           300\n",
      "13  1956         5127          893         302           293           298\n",
      "14  1960         8119          911         309           294           308\n",
      "15  1964         7702         1029         347           339           343\n",
      "16  1968         8588         1057         359           340           358\n",
      "17  1972        10304         1215         404           392           419\n",
      "18  1976         8641         1320         438           434           448\n",
      "19  1980         7191         1384         457           458           469\n",
      "20  1984         9454         1476         497           477           502\n",
      "21  1988        12037         1582         520           513           549\n",
      "22  1992        12977         1712         559           549           604\n",
      "23  1996        13780         1842         608           605           629\n",
      "24  2000        13821         2004         663           661           680\n",
      "25  2004        13443         2001         664           660           677\n",
      "26  2008        13602         2048         671           667           710\n",
      "27  2012        12920         1941         632           630           679\n",
      "28  2016        13688         2023         665           655           703\n"
     ]
    }
   ],
   "source": [
    "print(summer_medal_count_new)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "blocked-newspaper",
   "metadata": {},
   "source": [
    "I then calculate the Pearon correlation coefficient between the total number of medals in the winter and summer olympics from 1924 to 2016."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "regional-netherlands",
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "cognitive-hello",
   "metadata": {},
   "outputs": [],
   "source": [
    "x_simple = winter_medal_count.medal_count\n",
    "y_simple = summer_medal_count_new.medal_count\n",
    "my_rho = np.corrcoef(x_simple, y_simple)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "hidden-tragedy",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "[[1.         0.94141801]\n",
      " [0.94141801 1.        ]]\n"
     ]
    }
   ],
   "source": [
    "print(my_rho)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "proprietary-probe",
   "metadata": {},
   "source": [
    "The Pearon correlation coefficient between the total number of medals in the winter and summer olympics from 1924 to 2016, is 0.94, which is highly positive. Therefore, the performance of a country in winter olympics is highly correlated to that in summer olympics"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "related-celtic",
   "metadata": {},
   "source": [
    "I will then calculate the standard deviation in country performance through years.  A Comparison between average std of Winter and that of  Summer Olympics will help."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "talented-foundation",
   "metadata": {},
   "outputs": [],
   "source": [
    "std_medal_count_summer_olympics = np.std(y_simple)\n",
    "std_medal_count_winter_olympics = np.std(x_simple)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "unlike-tackle",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "std_medal_count_summer_olympics = 475.323015441357\n",
      "std_medal_count_winter_olympics = 152.56899942903493\n"
     ]
    }
   ],
   "source": [
    "print(\"std_medal_count_summer_olympics =\",std_medal_count_summer_olympics)\n",
    "print(\"std_medal_count_winter_olympics =\",std_medal_count_winter_olympics)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "personalized-forum",
   "metadata": {},
   "source": [
    "From 1924 to 2016, as the standard deviation in the summer olympics is about 3 times that in the winter olympics,  country performance by year change more in  Summer Olympics."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "critical-society",
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.7"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}# Milestone-3
