{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "This jupyter notebook will serve as the notebook for your capstone project. Each week we will add new sections to the this notebook and you will submit the entire notebook for the weekly assignment. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Introduction"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The project is on ASD screening of toddlers. ASD is Autistic Spectrum Disorder. As it is been found that Clinics to detect Autism in toddlers are less and parents need to take appointments which result in waiting period of 1 or 2 months. Every time its not necessary that a child will have Autism just because their parents want to confirm. It is waste of money and time for parents. To save the time and money there are some pre-screening process that can be done. In the pre-screening process, we can ask parents some questions and depending on those questions we can predict that a child needs to be sent to clinic for further diagnosis. The pre-screening process should be done by parents and answer questions related to their childâ€™s behavior and different activities. In this way not every child and parent will be suffered in the long waiting period of clinic. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Dataset"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The data used is originally from Kaggle repository(https://www.kaggle.com/fabdelja/autism-screening-for-toddlers#Toddler%20Autism%20dataset%20July%202018.csv). The data consists of around 1000 observations of toddlers from ASD screening centers for Autism."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Project Definition"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "To Predict if a toddler is showing traits for Autism so that he/she should go for further ASD diagnosis clinic."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Data Exploration"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 844,
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "import pandas as pd"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Load csv file"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 845,
   "metadata": {},
   "outputs": [],
   "source": [
    "df = pd.read_csv('/Users/karis/Toddler Autism dataset July 2018.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 846,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Case_No</th>\n",
       "      <th>A1</th>\n",
       "      <th>A2</th>\n",
       "      <th>A3</th>\n",
       "      <th>A4</th>\n",
       "      <th>A5</th>\n",
       "      <th>A6</th>\n",
       "      <th>A7</th>\n",
       "      <th>A8</th>\n",
       "      <th>A9</th>\n",
       "      <th>A10</th>\n",
       "      <th>Age_Mons</th>\n",
       "      <th>Qchat-10-Score</th>\n",
       "      <th>Sex</th>\n",
       "      <th>Ethnicity</th>\n",
       "      <th>Jaundice</th>\n",
       "      <th>Family_mem_with_ASD</th>\n",
       "      <th>Who completed the test</th>\n",
       "      <th>Class/ASD Traits</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>28</td>\n",
       "      <td>3</td>\n",
       "      <td>f</td>\n",
       "      <td>middle eastern</td>\n",
       "      <td>yes</td>\n",
       "      <td>no</td>\n",
       "      <td>family member</td>\n",
       "      <td>No</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>36</td>\n",
       "      <td>4</td>\n",
       "      <td>m</td>\n",
       "      <td>White European</td>\n",
       "      <td>yes</td>\n",
       "      <td>no</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>36</td>\n",
       "      <td>4</td>\n",
       "      <td>m</td>\n",
       "      <td>middle eastern</td>\n",
       "      <td>yes</td>\n",
       "      <td>no</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>24</td>\n",
       "      <td>10</td>\n",
       "      <td>m</td>\n",
       "      <td>Hispanic</td>\n",
       "      <td>no</td>\n",
       "      <td>no</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>20</td>\n",
       "      <td>9</td>\n",
       "      <td>f</td>\n",
       "      <td>White European</td>\n",
       "      <td>no</td>\n",
       "      <td>yes</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Case_No  A1  A2  A3  A4  A5  A6  A7  A8  A9  A10  Age_Mons  Qchat-10-Score  \\\n",
       "0        1   0   0   0   0   0   0   1   1   0    1        28               3   \n",
       "1        2   1   1   0   0   0   1   1   0   0    0        36               4   \n",
       "2        3   1   0   0   0   0   0   1   1   0    1        36               4   \n",
       "3        4   1   1   1   1   1   1   1   1   1    1        24              10   \n",
       "4        5   1   1   0   1   1   1   1   1   1    1        20               9   \n",
       "\n",
       "  Sex       Ethnicity Jaundice Family_mem_with_ASD Who completed the test  \\\n",
       "0   f  middle eastern      yes                  no          family member   \n",
       "1   m  White European      yes                  no          family member   \n",
       "2   m  middle eastern      yes                  no          family member   \n",
       "3   m        Hispanic       no                  no          family member   \n",
       "4   f  White European       no                 yes          family member   \n",
       "\n",
       "  Class/ASD Traits   \n",
       "0                No  \n",
       "1               Yes  \n",
       "2               Yes  \n",
       "3               Yes  \n",
       "4               Yes  "
      ]
     },
     "execution_count": 846,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Total rows and columns."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 847,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(1054, 19)"
      ]
     },
     "execution_count": 847,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Changing the name of column 18 to 'Detected' as its an important feature. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 848,
   "metadata": {},
   "outputs": [],
   "source": [
    "df=df.rename(columns={ df.columns[18]: \"Detected\"})"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Checking for Null values in the dataset"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 849,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Case_No                   0\n",
       "A1                        0\n",
       "A2                        0\n",
       "A3                        0\n",
       "A4                        0\n",
       "A5                        0\n",
       "A6                        0\n",
       "A7                        0\n",
       "A8                        0\n",
       "A9                        0\n",
       "A10                       0\n",
       "Age_Mons                  0\n",
       "Qchat-10-Score            0\n",
       "Sex                       0\n",
       "Ethnicity                 0\n",
       "Jaundice                  0\n",
       "Family_mem_with_ASD       0\n",
       "Who completed the test    0\n",
       "Detected                  0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 849,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.isna().sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "There are no Null values in the dataset."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 850,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Case_No</th>\n",
       "      <th>A1</th>\n",
       "      <th>A2</th>\n",
       "      <th>A3</th>\n",
       "      <th>A4</th>\n",
       "      <th>A5</th>\n",
       "      <th>A6</th>\n",
       "      <th>A7</th>\n",
       "      <th>A8</th>\n",
       "      <th>A9</th>\n",
       "      <th>A10</th>\n",
       "      <th>Age_Mons</th>\n",
       "      <th>Qchat-10-Score</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1054.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>527.500000</td>\n",
       "      <td>0.563567</td>\n",
       "      <td>0.448767</td>\n",
       "      <td>0.401328</td>\n",
       "      <td>0.512334</td>\n",
       "      <td>0.524668</td>\n",
       "      <td>0.576850</td>\n",
       "      <td>0.649905</td>\n",
       "      <td>0.459203</td>\n",
       "      <td>0.489564</td>\n",
       "      <td>0.586338</td>\n",
       "      <td>27.867173</td>\n",
       "      <td>5.212524</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>304.407895</td>\n",
       "      <td>0.496178</td>\n",
       "      <td>0.497604</td>\n",
       "      <td>0.490400</td>\n",
       "      <td>0.500085</td>\n",
       "      <td>0.499628</td>\n",
       "      <td>0.494293</td>\n",
       "      <td>0.477226</td>\n",
       "      <td>0.498569</td>\n",
       "      <td>0.500128</td>\n",
       "      <td>0.492723</td>\n",
       "      <td>7.980354</td>\n",
       "      <td>2.907304</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>12.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>264.250000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>23.000000</td>\n",
       "      <td>3.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>527.500000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>30.000000</td>\n",
       "      <td>5.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>790.750000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>36.000000</td>\n",
       "      <td>8.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>1054.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>36.000000</td>\n",
       "      <td>10.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "           Case_No           A1           A2           A3           A4  \\\n",
       "count  1054.000000  1054.000000  1054.000000  1054.000000  1054.000000   \n",
       "mean    527.500000     0.563567     0.448767     0.401328     0.512334   \n",
       "std     304.407895     0.496178     0.497604     0.490400     0.500085   \n",
       "min       1.000000     0.000000     0.000000     0.000000     0.000000   \n",
       "25%     264.250000     0.000000     0.000000     0.000000     0.000000   \n",
       "50%     527.500000     1.000000     0.000000     0.000000     1.000000   \n",
       "75%     790.750000     1.000000     1.000000     1.000000     1.000000   \n",
       "max    1054.000000     1.000000     1.000000     1.000000     1.000000   \n",
       "\n",
       "                A5           A6           A7           A8           A9  \\\n",
       "count  1054.000000  1054.000000  1054.000000  1054.000000  1054.000000   \n",
       "mean      0.524668     0.576850     0.649905     0.459203     0.489564   \n",
       "std       0.499628     0.494293     0.477226     0.498569     0.500128   \n",
       "min       0.000000     0.000000     0.000000     0.000000     0.000000   \n",
       "25%       0.000000     0.000000     0.000000     0.000000     0.000000   \n",
       "50%       1.000000     1.000000     1.000000     0.000000     0.000000   \n",
       "75%       1.000000     1.000000     1.000000     1.000000     1.000000   \n",
       "max       1.000000     1.000000     1.000000     1.000000     1.000000   \n",
       "\n",
       "               A10     Age_Mons  Qchat-10-Score  \n",
       "count  1054.000000  1054.000000     1054.000000  \n",
       "mean      0.586338    27.867173        5.212524  \n",
       "std       0.492723     7.980354        2.907304  \n",
       "min       0.000000    12.000000        0.000000  \n",
       "25%       0.000000    23.000000        3.000000  \n",
       "50%       1.000000    30.000000        5.000000  \n",
       "75%       1.000000    36.000000        8.000000  \n",
       "max       1.000000    36.000000       10.000000  "
      ]
     },
     "execution_count": 850,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 851,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Number of samples: 1054\n"
     ]
    }
   ],
   "source": [
    "print('Number of samples:',len(df))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 852,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Detected\n",
       "No     326\n",
       "Yes    728\n",
       "dtype: int64"
      ]
     },
     "execution_count": 852,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.groupby('Detected').size()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Creating positive and negative class of dataset in 'OUTPUT_LABEL'. '0' is for negative class and '1' is for positive class."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 853,
   "metadata": {
    "scrolled": true
   },
   "outputs": [],
   "source": [
    "df['OUTPUT_LABEL'] = (df.Detected=='Yes').astype('int')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 854,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "OUTPUT_LABEL\n",
       "0    326\n",
       "1    728\n",
       "dtype: int64"
      ]
     },
     "execution_count": 854,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.groupby('OUTPUT_LABEL').size()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 855,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>OUTPUT_LABEL</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   OUTPUT_LABEL\n",
       "0             0\n",
       "1             1\n",
       "2             1\n",
       "3             1\n",
       "4             1"
      ]
     },
     "execution_count": 855,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[['OUTPUT_LABEL']].head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Calculating the prevalence of positive class."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 856,
   "metadata": {},
   "outputs": [],
   "source": [
    "def calc_prevalence(y_actual):\n",
    "    # this function calculates the prevalence of the positive class (label = 1)\n",
    "    return (sum(y_actual)/len(y_actual))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 857,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "prevalence of the positive class: 0.691\n"
     ]
    }
   ],
   "source": [
    "print('prevalence of the positive class: %.3f'%calc_prevalence(df['OUTPUT_LABEL'].values))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "According to my dataset, I can say that 69.1% children show the traits of Autism based on different parameters and should be sent for further ASD screening process in clinic."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Describing columns and Unique Dataset."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 858,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Number of columns: 20\n"
     ]
    }
   ],
   "source": [
    "print('Number of columns:',len(df.columns))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 859,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['Case_No', 'A1', 'A2', 'A3', 'A4', 'A5', 'A6', 'A7', 'A8', 'A9', 'A10',\n",
       "       'Age_Mons', 'Qchat-10-Score', 'Sex', 'Ethnicity', 'Jaundice',\n",
       "       'Family_mem_with_ASD', 'Who completed the test', 'Detected',\n",
       "       'OUTPUT_LABEL'],\n",
       "      dtype='object')"
      ]
     },
     "execution_count": 859,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 860,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Case_No</th>\n",
       "      <th>A1</th>\n",
       "      <th>A2</th>\n",
       "      <th>A3</th>\n",
       "      <th>A4</th>\n",
       "      <th>A5</th>\n",
       "      <th>A6</th>\n",
       "      <th>A7</th>\n",
       "      <th>A8</th>\n",
       "      <th>A9</th>\n",
       "      <th>A10</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Case_No  A1  A2  A3  A4  A5  A6  A7  A8  A9  A10\n",
       "0        1   0   0   0   0   0   0   1   1   0    1\n",
       "1        2   1   1   0   0   0   1   1   0   0    0\n",
       "2        3   1   0   0   0   0   0   1   1   0    1\n",
       "3        4   1   1   1   1   1   1   1   1   1    1\n",
       "4        5   1   1   0   1   1   1   1   1   1    1"
      ]
     },
     "execution_count": 860,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[list(df.columns)[0:11]].head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 861,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Age_Mons</th>\n",
       "      <th>Qchat-10-Score</th>\n",
       "      <th>Sex</th>\n",
       "      <th>Ethnicity</th>\n",
       "      <th>Jaundice</th>\n",
       "      <th>Family_mem_with_ASD</th>\n",
       "      <th>Who completed the test</th>\n",
       "      <th>Detected</th>\n",
       "      <th>OUTPUT_LABEL</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>28</td>\n",
       "      <td>3</td>\n",
       "      <td>f</td>\n",
       "      <td>middle eastern</td>\n",
       "      <td>yes</td>\n",
       "      <td>no</td>\n",
       "      <td>family member</td>\n",
       "      <td>No</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>36</td>\n",
       "      <td>4</td>\n",
       "      <td>m</td>\n",
       "      <td>White European</td>\n",
       "      <td>yes</td>\n",
       "      <td>no</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>36</td>\n",
       "      <td>4</td>\n",
       "      <td>m</td>\n",
       "      <td>middle eastern</td>\n",
       "      <td>yes</td>\n",
       "      <td>no</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>24</td>\n",
       "      <td>10</td>\n",
       "      <td>m</td>\n",
       "      <td>Hispanic</td>\n",
       "      <td>no</td>\n",
       "      <td>no</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>20</td>\n",
       "      <td>9</td>\n",
       "      <td>f</td>\n",
       "      <td>White European</td>\n",
       "      <td>no</td>\n",
       "      <td>yes</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Age_Mons  Qchat-10-Score Sex       Ethnicity Jaundice Family_mem_with_ASD  \\\n",
       "0        28               3   f  middle eastern      yes                  no   \n",
       "1        36               4   m  White European      yes                  no   \n",
       "2        36               4   m  middle eastern      yes                  no   \n",
       "3        24              10   m        Hispanic       no                  no   \n",
       "4        20               9   f  White European       no                 yes   \n",
       "\n",
       "  Who completed the test Detected  OUTPUT_LABEL  \n",
       "0          family member       No             0  \n",
       "1          family member      Yes             1  \n",
       "2          family member      Yes             1  \n",
       "3          family member      Yes             1  \n",
       "4          family member      Yes             1  "
      ]
     },
     "execution_count": 861,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[list(df.columns)[11:22]].head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 862,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Who completed the test\n",
       "Health Care Professional      24\n",
       "Health care professional       5\n",
       "Others                         3\n",
       "Self                           4\n",
       "family member               1018\n",
       "dtype: int64"
      ]
     },
     "execution_count": 862,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.groupby('Who completed the test').size()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Unique Dataset:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 863,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Case_No: 1054 unique values\n",
      "A1\n",
      "[0 1]\n",
      "A2\n",
      "[0 1]\n",
      "A3\n",
      "[0 1]\n",
      "A4\n",
      "[0 1]\n",
      "A5\n",
      "[0 1]\n",
      "A6\n",
      "[0 1]\n",
      "A7\n",
      "[1 0]\n",
      "A8\n",
      "[1 0]\n",
      "A9\n",
      "[0 1]\n",
      "A10\n",
      "[1 0]\n",
      "Age_Mons\n",
      "[28 36 24 20 21 33 22 17 25 15 18 12 29 35 32 19 14 13 30 23 34 26 31 27\n",
      " 16]\n",
      "Qchat-10-Score\n",
      "[ 3  4 10  9  8  5  6  2  0  7  1]\n",
      "Sex\n",
      "['f' 'm']\n",
      "Ethnicity\n",
      "['middle eastern' 'White European' 'Hispanic' 'black' 'asian'\n",
      " 'south asian' 'Native Indian' 'Others' 'Latino' 'mixed' 'Pacifica']\n",
      "Jaundice\n",
      "['yes' 'no']\n",
      "Family_mem_with_ASD\n",
      "['no' 'yes']\n",
      "Who completed the test\n",
      "['family member' 'Health Care Professional' 'Health care professional'\n",
      " 'Self' 'Others']\n",
      "Detected\n",
      "['No' 'Yes']\n",
      "OUTPUT_LABEL\n",
      "[0 1]\n"
     ]
    }
   ],
   "source": [
    "# your code here\n",
    "# for each column\n",
    "for c in list(df.columns):\n",
    "    \n",
    "    # get a list of unique values\n",
    "    n = df[c].unique()\n",
    "    \n",
    "    # if number of unique values is less than 30, print the values. Otherwise print the number of unique values\n",
    "    if len(n)<30:\n",
    "        print(c)\n",
    "        print(n)\n",
    "    else:\n",
    "        print(c + ': ' +str(len(n)) + ' unique values')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The dataset has a mix of both categorical and numerical data. Let's explore more columns. \n",
    "There are 20 columns. \n",
    "The columns Named \"A1,A2....,A10\" are different questions asked to parents of the toddler at the initial screening. Based on the answer to these questions we got the Qchat-10-Score column. The answers were either yes or no and the values 1 or 0 were assigned to the respective answer. \n",
    "From analysis of the columns, we can see there are a mix of categorical (non-numeric) and numerical data. A few things to point out,\n",
    "Jaundice and Family_mem_with_ASD are categorial data but are important feature for prediction.\n",
    "Age_Mons and Who completed the test are not important feature of prediction.\n",
    "Case_No is a identifier."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Feature Engineering"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "In my dataset we describe the features of the data first. The features can be put in to categories based on our data set, which are Numerical features and Categorial(Non-numerical) features. In Feature Engineering process we create new outputs(features) for our data set using our exsisting features. This helps in when we have huge amount of data and we need only few features to define our predictive models. This helps us focus on only the highlighted data. Then , I have done one-hot encoding on 'Ethinicity' and showed Ordinal features of 'Q-chat-score'."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 864,
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 865,
   "metadata": {},
   "outputs": [],
   "source": [
    "# replace ? with nan\n",
    "df = df.replace('?',np.nan)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Numerical Features"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "These features are numerical. They do not need any changes. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 866,
   "metadata": {},
   "outputs": [],
   "source": [
    "cols_num = ['A1','A2','A3','A4','A5','A6','A7','A8','A9','A10','Age_Mons']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 867,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "A1          0\n",
       "A2          0\n",
       "A3          0\n",
       "A4          0\n",
       "A5          0\n",
       "A6          0\n",
       "A7          0\n",
       "A8          0\n",
       "A9          0\n",
       "A10         0\n",
       "Age_Mons    0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 867,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[cols_num].isnull().sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "No Missing values in Numerical features."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Categorical Features"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "They are non- numerical features like 'Sex' or 'Ethnicity' in my dataset. To convert them to numerical we use one-hot encoding."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 868,
   "metadata": {},
   "outputs": [],
   "source": [
    "cols_cat = ['Sex','Jaundice','Family_mem_with_ASD','Who completed the test']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 869,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Sex                       0\n",
       "Jaundice                  0\n",
       "Family_mem_with_ASD       0\n",
       "Who completed the test    0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 869,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[cols_cat].isnull().sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "No Missing values in categorial features."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "As we know to convert the categorial feature to numerical we need to do one-hot endcoding. But what features are important to us for lets check that. So, I have choosen 'Ethnicity' feature as it can be aan important feature."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 870,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Ethnicity: 11\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "Ethnicity\n",
       "White European    334\n",
       "asian             299\n",
       "middle eastern    188\n",
       "south asian        60\n",
       "black              53\n",
       "Hispanic           40\n",
       "Others             35\n",
       "Latino             26\n",
       "mixed               8\n",
       "Pacifica            8\n",
       "Native Indian       3\n",
       "dtype: int64"
      ]
     },
     "execution_count": 870,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "print('Ethnicity:', df.Ethnicity.nunique())\n",
    "df.groupby('Ethnicity').size().sort_values(ascending = False)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "There are 11 variables in 'Ethnicity feature'."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "In one-hot encoding, you create a new column for each unique value in that column. Then the value of the column is 1 if the sample has that unique value or 0 otherwise. For example, for the column Enticity, we would create new columns. We also did the same with coloumns Jaundice, Sex, Family_mem_with_ASD. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 871,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    middle eastern\n",
       "1    White European\n",
       "2    middle eastern\n",
       "3          Hispanic\n",
       "4    White European\n",
       "Name: Ethnicity, dtype: object"
      ]
     },
     "execution_count": 871,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.Ethnicity.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 872,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Ethnicity_Hispanic</th>\n",
       "      <th>Ethnicity_Latino</th>\n",
       "      <th>Ethnicity_Native Indian</th>\n",
       "      <th>Ethnicity_Others</th>\n",
       "      <th>Ethnicity_Pacifica</th>\n",
       "      <th>Ethnicity_White European</th>\n",
       "      <th>Ethnicity_asian</th>\n",
       "      <th>Ethnicity_black</th>\n",
       "      <th>Ethnicity_middle eastern</th>\n",
       "      <th>Ethnicity_mixed</th>\n",
       "      <th>Ethnicity_south asian</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Ethnicity_Hispanic  Ethnicity_Latino  Ethnicity_Native Indian  \\\n",
       "0                   0                 0                        0   \n",
       "1                   0                 0                        0   \n",
       "2                   0                 0                        0   \n",
       "3                   1                 0                        0   \n",
       "4                   0                 0                        0   \n",
       "\n",
       "   Ethnicity_Others  Ethnicity_Pacifica  Ethnicity_White European  \\\n",
       "0                 0                   0                         0   \n",
       "1                 0                   0                         1   \n",
       "2                 0                   0                         0   \n",
       "3                 0                   0                         0   \n",
       "4                 0                   0                         1   \n",
       "\n",
       "   Ethnicity_asian  Ethnicity_black  Ethnicity_middle eastern  \\\n",
       "0                0                0                         1   \n",
       "1                0                0                         0   \n",
       "2                0                0                         1   \n",
       "3                0                0                         0   \n",
       "4                0                0                         0   \n",
       "\n",
       "   Ethnicity_mixed  Ethnicity_south asian  \n",
       "0                0                      0  \n",
       "1                0                      0  \n",
       "2                0                      0  \n",
       "3                0                      0  \n",
       "4                0                      0  "
      ]
     },
     "execution_count": 872,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.get_dummies(df['Ethnicity'],prefix = 'Ethnicity').head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 873,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Ethnicity_Latino</th>\n",
       "      <th>Ethnicity_Native Indian</th>\n",
       "      <th>Ethnicity_Others</th>\n",
       "      <th>Ethnicity_Pacifica</th>\n",
       "      <th>Ethnicity_White European</th>\n",
       "      <th>Ethnicity_asian</th>\n",
       "      <th>Ethnicity_black</th>\n",
       "      <th>Ethnicity_middle eastern</th>\n",
       "      <th>Ethnicity_mixed</th>\n",
       "      <th>Ethnicity_south asian</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Ethnicity_Latino  Ethnicity_Native Indian  Ethnicity_Others  \\\n",
       "0                 0                        0                 0   \n",
       "1                 0                        0                 0   \n",
       "2                 0                        0                 0   \n",
       "3                 0                        0                 0   \n",
       "4                 0                        0                 0   \n",
       "\n",
       "   Ethnicity_Pacifica  Ethnicity_White European  Ethnicity_asian  \\\n",
       "0                   0                         0                0   \n",
       "1                   0                         1                0   \n",
       "2                   0                         0                0   \n",
       "3                   0                         0                0   \n",
       "4                   0                         1                0   \n",
       "\n",
       "   Ethnicity_black  Ethnicity_middle eastern  Ethnicity_mixed  \\\n",
       "0                0                         1                0   \n",
       "1                0                         0                0   \n",
       "2                0                         1                0   \n",
       "3                0                         0                0   \n",
       "4                0                         0                0   \n",
       "\n",
       "   Ethnicity_south asian  \n",
       "0                      0  \n",
       "1                      0  \n",
       "2                      0  \n",
       "3                      0  \n",
       "4                      0  "
      ]
     },
     "execution_count": 873,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.get_dummies(df['Ethnicity'],prefix = 'Ethnicity', drop_first = True).head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We send all the columns at once into the get_dummies function and use the column name as the prefix."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 874,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Sex_m</th>\n",
       "      <th>Jaundice_yes</th>\n",
       "      <th>Family_mem_with_ASD_yes</th>\n",
       "      <th>Who completed the test_Health care professional</th>\n",
       "      <th>Who completed the test_Others</th>\n",
       "      <th>Who completed the test_Self</th>\n",
       "      <th>Who completed the test_family member</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Sex_m  Jaundice_yes  Family_mem_with_ASD_yes  \\\n",
       "0      0             1                        0   \n",
       "1      1             1                        0   \n",
       "2      1             1                        0   \n",
       "3      1             0                        0   \n",
       "4      0             0                        1   \n",
       "\n",
       "   Who completed the test_Health care professional  \\\n",
       "0                                                0   \n",
       "1                                                0   \n",
       "2                                                0   \n",
       "3                                                0   \n",
       "4                                                0   \n",
       "\n",
       "   Who completed the test_Others  Who completed the test_Self  \\\n",
       "0                              0                            0   \n",
       "1                              0                            0   \n",
       "2                              0                            0   \n",
       "3                              0                            0   \n",
       "4                              0                            0   \n",
       "\n",
       "   Who completed the test_family member  \n",
       "0                                     1  \n",
       "1                                     1  \n",
       "2                                     1  \n",
       "3                                     1  \n",
       "4                                     1  "
      ]
     },
     "execution_count": 874,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.get_dummies(df[cols_cat],drop_first = True).head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Now we are ready to make all of our categorical features"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 875,
   "metadata": {},
   "outputs": [],
   "source": [
    "df_cat = pd.get_dummies(df[cols_cat],drop_first = True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 876,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Sex_m</th>\n",
       "      <th>Jaundice_yes</th>\n",
       "      <th>Family_mem_with_ASD_yes</th>\n",
       "      <th>Who completed the test_Health care professional</th>\n",
       "      <th>Who completed the test_Others</th>\n",
       "      <th>Who completed the test_Self</th>\n",
       "      <th>Who completed the test_family member</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Sex_m  Jaundice_yes  Family_mem_with_ASD_yes  \\\n",
       "0      0             1                        0   \n",
       "1      1             1                        0   \n",
       "2      1             1                        0   \n",
       "3      1             0                        0   \n",
       "4      0             0                        1   \n",
       "\n",
       "   Who completed the test_Health care professional  \\\n",
       "0                                                0   \n",
       "1                                                0   \n",
       "2                                                0   \n",
       "3                                                0   \n",
       "4                                                0   \n",
       "\n",
       "   Who completed the test_Others  Who completed the test_Self  \\\n",
       "0                              0                            0   \n",
       "1                              0                            0   \n",
       "2                              0                            0   \n",
       "3                              0                            0   \n",
       "4                              0                            0   \n",
       "\n",
       "   Who completed the test_family member  \n",
       "0                                     1  \n",
       "1                                     1  \n",
       "2                                     1  \n",
       "3                                     1  \n",
       "4                                     1  "
      ]
     },
     "execution_count": 876,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_cat.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "To add the one-hot encoding columns to the dataframe we can use concat function. Make sure to use axis = 1 to indicate add the columns."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 877,
   "metadata": {},
   "outputs": [],
   "source": [
    "df = pd.concat([df,df_cat], axis = 1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 878,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Case_No</th>\n",
       "      <th>A1</th>\n",
       "      <th>A2</th>\n",
       "      <th>A3</th>\n",
       "      <th>A4</th>\n",
       "      <th>A5</th>\n",
       "      <th>A6</th>\n",
       "      <th>A7</th>\n",
       "      <th>A8</th>\n",
       "      <th>A9</th>\n",
       "      <th>...</th>\n",
       "      <th>Who completed the test</th>\n",
       "      <th>Detected</th>\n",
       "      <th>OUTPUT_LABEL</th>\n",
       "      <th>Sex_m</th>\n",
       "      <th>Jaundice_yes</th>\n",
       "      <th>Family_mem_with_ASD_yes</th>\n",
       "      <th>Who completed the test_Health care professional</th>\n",
       "      <th>Who completed the test_Others</th>\n",
       "      <th>Who completed the test_Self</th>\n",
       "      <th>Who completed the test_family member</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>family member</td>\n",
       "      <td>No</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>...</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>...</td>\n",
       "      <td>family member</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows Ã— 27 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   Case_No  A1  A2  A3  A4  A5  A6  A7  A8  A9  \\\n",
       "0        1   0   0   0   0   0   0   1   1   0   \n",
       "1        2   1   1   0   0   0   1   1   0   0   \n",
       "2        3   1   0   0   0   0   0   1   1   0   \n",
       "3        4   1   1   1   1   1   1   1   1   1   \n",
       "4        5   1   1   0   1   1   1   1   1   1   \n",
       "\n",
       "                   ...                   Who completed the test  Detected  \\\n",
       "0                  ...                            family member        No   \n",
       "1                  ...                            family member       Yes   \n",
       "2                  ...                            family member       Yes   \n",
       "3                  ...                            family member       Yes   \n",
       "4                  ...                            family member       Yes   \n",
       "\n",
       "   OUTPUT_LABEL Sex_m Jaundice_yes Family_mem_with_ASD_yes  \\\n",
       "0             0     0            1                       0   \n",
       "1             1     1            1                       0   \n",
       "2             1     1            1                       0   \n",
       "3             1     1            0                       0   \n",
       "4             1     0            0                       1   \n",
       "\n",
       "  Who completed the test_Health care professional  \\\n",
       "0                                               0   \n",
       "1                                               0   \n",
       "2                                               0   \n",
       "3                                               0   \n",
       "4                                               0   \n",
       "\n",
       "  Who completed the test_Others Who completed the test_Self  \\\n",
       "0                             0                           0   \n",
       "1                             0                           0   \n",
       "2                             0                           0   \n",
       "3                             0                           0   \n",
       "4                             0                           0   \n",
       "\n",
       "   Who completed the test_family member  \n",
       "0                                     1  \n",
       "1                                     1  \n",
       "2                                     1  \n",
       "3                                     1  \n",
       "4                                     1  \n",
       "\n",
       "[5 rows x 27 columns]"
      ]
     },
     "execution_count": 878,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 879,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['Case_No', 'A1', 'A2', 'A3', 'A4', 'A5', 'A6', 'A7', 'A8', 'A9', 'A10',\n",
       "       'Age_Mons', 'Qchat-10-Score', 'Sex', 'Ethnicity', 'Jaundice',\n",
       "       'Family_mem_with_ASD', 'Who completed the test', 'Detected',\n",
       "       'OUTPUT_LABEL', 'Sex_m', 'Jaundice_yes', 'Family_mem_with_ASD_yes',\n",
       "       'Who completed the test_Health care professional',\n",
       "       'Who completed the test_Others', 'Who completed the test_Self',\n",
       "       'Who completed the test_family member'],\n",
       "      dtype='object')"
      ]
     },
     "execution_count": 879,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.columns"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Save the column names of the categorical data."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 880,
   "metadata": {},
   "outputs": [],
   "source": [
    "cols_all_cat = list(df_cat.columns)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Ordinal Features"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "In column Qchat-10-Score, you would think of these as numerical data, but they are categorical in this dataset as shown below."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 881,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0     3\n",
       "1     4\n",
       "2     4\n",
       "3    10\n",
       "4     9\n",
       "Name: Qchat-10-Score, dtype: int64"
      ]
     },
     "execution_count": 881,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['Qchat-10-Score'].head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 882,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Qchat-10-Score\n",
       "0      54\n",
       "1      88\n",
       "2      88\n",
       "3      96\n",
       "4     110\n",
       "5     120\n",
       "6      96\n",
       "7     135\n",
       "8      97\n",
       "9      95\n",
       "10     75\n",
       "dtype: int64"
      ]
     },
     "execution_count": 882,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.groupby('Qchat-10-Score').size()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Engineering Features Summary"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 883,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Total number of features: 18\n",
      "Numerical Features: 11\n",
      "Categorical Features: 7\n"
     ]
    }
   ],
   "source": [
    "print('Total number of features:', len(cols_num + cols_all_cat))\n",
    "print('Numerical Features:',len(cols_num))\n",
    "print('Categorical Features:',len(cols_all_cat))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Let's check if we are missing any data. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 884,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Who completed the test_family member    0\n",
       "Who completed the test_Self             0\n",
       "A2                                      0\n",
       "A3                                      0\n",
       "A4                                      0\n",
       "A5                                      0\n",
       "A6                                      0\n",
       "A7                                      0\n",
       "A8                                      0\n",
       "A9                                      0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 884,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[cols_num + cols_all_cat ].isnull().sum().sort_values(ascending = False).head(10)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Making a new dataframe that has important columns. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 885,
   "metadata": {},
   "outputs": [],
   "source": [
    "cols_input = cols_num + cols_all_cat\n",
    "df_data = df[cols_input + ['OUTPUT_LABEL']]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 886,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Case_No                                            1054\n",
      "A1                                                    2\n",
      "A2                                                    2\n",
      "A3                                                    2\n",
      "A4                                                    2\n",
      "A5                                                    2\n",
      "A6                                                    2\n",
      "A7                                                    2\n",
      "A8                                                    2\n",
      "A9                                                    2\n",
      "A10                                                   2\n",
      "Age_Mons                                             25\n",
      "Qchat-10-Score                                       11\n",
      "Sex                                                   2\n",
      "Ethnicity                                            11\n",
      "Jaundice                                              2\n",
      "Family_mem_with_ASD                                   2\n",
      "Who completed the test                                5\n",
      "Detected                                              2\n",
      "OUTPUT_LABEL                                          2\n",
      "Sex_m                                                 2\n",
      "Jaundice_yes                                          2\n",
      "Family_mem_with_ASD_yes                               2\n",
      "Who completed the test_Health care professional       2\n",
      "Who completed the test_Others                         2\n",
      "Who completed the test_Self                           2\n",
      "Who completed the test_family member                  2\n",
      "dtype: int64\n"
     ]
    }
   ],
   "source": [
    "print(df.nunique())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 887,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Case_No                                            0\n",
       "A1                                                 0\n",
       "A2                                                 0\n",
       "A3                                                 0\n",
       "A4                                                 0\n",
       "A5                                                 0\n",
       "A6                                                 0\n",
       "A7                                                 0\n",
       "A8                                                 0\n",
       "A9                                                 0\n",
       "A10                                                0\n",
       "Age_Mons                                           0\n",
       "Qchat-10-Score                                     0\n",
       "Sex                                                0\n",
       "Ethnicity                                          0\n",
       "Jaundice                                           0\n",
       "Family_mem_with_ASD                                0\n",
       "Who completed the test                             0\n",
       "Detected                                           0\n",
       "OUTPUT_LABEL                                       0\n",
       "Sex_m                                              0\n",
       "Jaundice_yes                                       0\n",
       "Family_mem_with_ASD_yes                            0\n",
       "Who completed the test_Health care professional    0\n",
       "Who completed the test_Others                      0\n",
       "Who completed the test_Self                        0\n",
       "Who completed the test_family member               0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 887,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.isna().sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Check a few things to catch known bugs. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 888,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "set()\n"
     ]
    }
   ],
   "source": [
    "# check for duplicated columns in cols_input\n",
    "dup_cols = set([x for x in cols_input if cols_input.count(x) > 1])\n",
    "print(dup_cols)\n",
    "assert len(dup_cols) == 0,'you have duplicated columns in cols_input'"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 889,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "set()\n"
     ]
    }
   ],
   "source": [
    "# check for duplicated columns in df_data\n",
    "cols_df_data = list(df_data.columns)\n",
    "dup_cols = set([x for x in cols_df_data if cols_df_data.count(x) > 1])\n",
    "print(dup_cols)\n",
    "assert len(dup_cols) == 0,'you have duplicated columns in df_data'"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 890,
   "metadata": {},
   "outputs": [],
   "source": [
    "# check the size of df_data makes sense\n",
    "assert (len(cols_input) + 1) == len(df_data.columns), 'issue with dimensions of df_data or cols_input'"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Building Training/Validation/Test Samples"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Training test samples are used to fit the model.\n",
    "Validation samples are used for providing an unbiased evaluation of model fit on the training sample.\n",
    "Test samples are used for providing final unbiased evaluation of model fit."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 2: Create a training (df_train_all), validation (df_valid) and test (df_test) set. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 891,
   "metadata": {},
   "outputs": [],
   "source": [
    "# shuffle the samples\n",
    "df_data = df_data.sample(n = len(df_data), random_state = 42)\n",
    "df_data = df_data.reset_index(drop = True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 892,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Split size: 0.300\n"
     ]
    }
   ],
   "source": [
    "# Save 30% of the data as validation and test data \n",
    "df_valid_test=df_data.sample(frac=0.30,random_state=42)\n",
    "print('Split size: %.3f'%(len(df_valid_test)/len(df_data)))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 893,
   "metadata": {},
   "outputs": [],
   "source": [
    "df_test = df_valid_test.sample(frac = 0.5, random_state = 42)\n",
    "df_valid = df_valid_test.drop(df_test.index)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 894,
   "metadata": {},
   "outputs": [],
   "source": [
    "# use the rest of the data as training data\n",
    "df_train_all=df_data.drop(df_valid_test.index)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Ckeck the prevalence:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 895,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Test prevalence(n = 158):0.734\n",
      "Valid prevalence(n = 158):0.684\n",
      "Train all prevalence(n = 738):0.683\n"
     ]
    }
   ],
   "source": [
    "print('Test prevalence(n = %d):%.3f'%(len(df_test),calc_prevalence(df_test.OUTPUT_LABEL.values)))\n",
    "print('Valid prevalence(n = %d):%.3f'%(len(df_valid),calc_prevalence(df_valid.OUTPUT_LABEL.values)))\n",
    "print('Train all prevalence(n = %d):%.3f'%(len(df_train_all), calc_prevalence(df_train_all.OUTPUT_LABEL.values)))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Verifying that we used all the data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 896,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "all samples (n = 1054)\n"
     ]
    }
   ],
   "source": [
    "print('all samples (n = %d)'%len(df_data))\n",
    "assert len(df_data) == (len(df_test)+len(df_valid)+len(df_train_all)),'math didnt work'"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 2: take your df_train_all and create a balanced dataset. Briefly explain in your own words why we need to balance and a few techniques for balancing the dataset. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Balancing the dataset will give us unbiased results as the samples will have proportionate of both negative and positive values.\n",
    "\n",
    "Techniques used for balancing dataset are: Sub sampling Over sampling Creating synthetic samples"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 897,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Train balanced prevalence(n = 468):0.500\n"
     ]
    }
   ],
   "source": [
    "# split the training data into positive and negative\n",
    "rows_pos = df_train_all.OUTPUT_LABEL == 1\n",
    "df_train_pos = df_train_all.loc[rows_pos]\n",
    "df_train_neg = df_train_all.loc[~rows_pos]\n",
    "n = np.min([len(df_train_pos), len(df_train_neg)])\n",
    "\n",
    "# merge the balanced data\n",
    "df_train = pd.concat([df_train_pos.sample(n = n, random_state = 42), \n",
    "                      df_train_neg.sample(n = n, random_state = 42)],axis = 0, \n",
    "                     ignore_index = True)\n",
    "\n",
    "# shuffle the order of training samples \n",
    "df_train = df_train.sample(n = len(df_train), random_state = 42).reset_index(drop = True)\n",
    "\n",
    "print('Train balanced prevalence(n = %d):%.3f'%(len(df_train), calc_prevalence(df_train.OUTPUT_LABEL.values)))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 2: Save all 4 dataframes to csv and the cols_input"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 898,
   "metadata": {},
   "outputs": [],
   "source": [
    "df_train_all.to_csv('df_train_all.csv',index=False)\n",
    "df_train.to_csv('df_train.csv',index=False)\n",
    "df_valid.to_csv('df_valid.csv',index=False)\n",
    "df_test.to_csv('df_test.csv',index=False)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 899,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pickle\n",
    "pickle.dump(cols_input, open('cols_input.sav', 'wb'))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 2: fill any missing values with the mean value"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 900,
   "metadata": {},
   "outputs": [],
   "source": [
    "def fill_my_missing(df, df_mean, col2use):\n",
    "    # This function fills the missing values\n",
    "\n",
    "    # check the columns are present\n",
    "    for c in col2use:\n",
    "        assert c in df.columns, c + ' not in df'\n",
    "        assert c in df_mean.col.values, c+ 'not in df_mean'\n",
    "    \n",
    "    # replace the mean \n",
    "    for c in col2use:\n",
    "        mean_value = df_mean.loc[df_mean.col == c,'mean_val'].values[0]\n",
    "        df[c] = df[c].fillna(mean_value)\n",
    "    return df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 901,
   "metadata": {},
   "outputs": [],
   "source": [
    "df_mean = df_train_all[cols_input].mean(axis = 0)\n",
    "# save the means\n",
    "df_mean.to_csv('df_mean.csv',index=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 902,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>col</th>\n",
       "      <th>mean_val</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>A1</td>\n",
       "      <td>0.563686</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>A2</td>\n",
       "      <td>0.434959</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>A3</td>\n",
       "      <td>0.391599</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>A4</td>\n",
       "      <td>0.494580</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>A5</td>\n",
       "      <td>0.525745</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  col  mean_val\n",
       "0  A1  0.563686\n",
       "1  A2  0.434959\n",
       "2  A3  0.391599\n",
       "3  A4  0.494580\n",
       "4  A5  0.525745"
      ]
     },
     "execution_count": 902,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# load the means so we know how to do it for the test data\n",
    "df_mean_in = pd.read_csv('df_mean.csv', names =['col','mean_val'])\n",
    "df_mean_in.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 903,
   "metadata": {},
   "outputs": [],
   "source": [
    "df_train_all = fill_my_missing(df_train_all, df_mean_in, cols_input)\n",
    "df_train = fill_my_missing(df_train, df_mean_in, cols_input)\n",
    "df_valid = fill_my_missing(df_valid, df_mean_in, cols_input)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 904,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Training All shapes: (738, 18)\n",
      "Training shapes: (468, 18) (468,)\n",
      "Validation shapes: (158, 18) (158,)\n"
     ]
    }
   ],
   "source": [
    "X_train = df_train[cols_input].values\n",
    "X_train_all = df_train_all[cols_input].values\n",
    "X_valid = df_valid[cols_input].values\n",
    "\n",
    "y_train = df_train['OUTPUT_LABEL'].values\n",
    "y_valid = df_valid['OUTPUT_LABEL'].values\n",
    "\n",
    "print('Training All shapes:',X_train_all.shape)\n",
    "print('Training shapes:',X_train.shape, y_train.shape)\n",
    "print('Validation shapes:',X_valid.shape, y_valid.shape)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 2: create a scalar, save it, and scale the X matrices"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 905,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\sklearn\\utils\\validation.py:475: DataConversionWarning: Data with input dtype int64 was converted to float64 by StandardScaler.\n",
      "  warnings.warn(msg, DataConversionWarning)\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "StandardScaler(copy=True, with_mean=True, with_std=True)"
      ]
     },
     "execution_count": 905,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.preprocessing import StandardScaler\n",
    "\n",
    "scaler  = StandardScaler()\n",
    "scaler.fit(X_train_all)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 906,
   "metadata": {},
   "outputs": [],
   "source": [
    "scalerfile = 'scaler.sav'\n",
    "pickle.dump(scaler, open(scalerfile, 'wb'))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 907,
   "metadata": {},
   "outputs": [],
   "source": [
    "# load it back\n",
    "scaler = pickle.load(open(scalerfile, 'rb'))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 908,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\sklearn\\utils\\validation.py:475: DataConversionWarning: Data with input dtype int64 was converted to float64 by StandardScaler.\n",
      "  warnings.warn(msg, DataConversionWarning)\n",
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\sklearn\\utils\\validation.py:475: DataConversionWarning: Data with input dtype int64 was converted to float64 by StandardScaler.\n",
      "  warnings.warn(msg, DataConversionWarning)\n"
     ]
    }
   ],
   "source": [
    "# transform our data matrices\n",
    "X_train_tf = scaler.transform(X_train)\n",
    "X_valid_tf = scaler.transform(X_valid)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Model Selection "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 909,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.metrics import roc_auc_score, accuracy_score, precision_score, recall_score\n",
    "def calc_specificity(y_actual, y_pred, thresh):\n",
    "    # calculates specificity\n",
    "    return sum((y_pred < thresh) & (y_actual == 0)) /sum(y_actual ==0)\n",
    "\n",
    "def print_report(y_actual, y_pred, thresh):\n",
    "    \n",
    "    auc = roc_auc_score(y_actual, y_pred)\n",
    "    accuracy = accuracy_score(y_actual, (y_pred > thresh))\n",
    "    recall = recall_score(y_actual, (y_pred > thresh))\n",
    "    precision = precision_score(y_actual, (y_pred > thresh))\n",
    "    specificity = calc_specificity(y_actual, y_pred, thresh)\n",
    "    print('AUC:%.3f'%auc)\n",
    "    print('accuracy:%.3f'%accuracy)\n",
    "    print('recall:%.3f'%recall)\n",
    "    print('precision:%.3f'%precision)\n",
    "    print('specificity:%.3f'%specificity)\n",
    "    print('prevalence:%.3f'%calc_prevalence(y_actual))\n",
    "    print(' ')\n",
    "    return auc, accuracy, recall, precision, specificity "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Since we balanced our training data, let's set our threshold at 0.5 to label a predicted sample as positive. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 910,
   "metadata": {},
   "outputs": [],
   "source": [
    "thresh = 0.5"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Model Selection: baseline models"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### K nearest neighbors (KNN)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The KNN Nearest Neighbors algorithm is used for Classification. It is commonly used because it is easy to interpret, and it take less time to calculate. It is based on feature similarity. An item is classified by a majority vote of its neighbors, with the item being allocated to the class most basic among its k closest neighbors. It is simple, versatile, no assumptions of data and has high accuracy."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "training a KNN model to evaluate performance."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 911,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "KNeighborsClassifier(algorithm='auto', leaf_size=30, metric='minkowski',\n",
       "           metric_params=None, n_jobs=1, n_neighbors=5, p=2,\n",
       "           weights='uniform')"
      ]
     },
     "execution_count": 911,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# k-nearest neighbors\n",
    "from sklearn.neighbors import KNeighborsClassifier\n",
    "knn=KNeighborsClassifier(n_neighbors = 5)\n",
    "knn.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 912,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "KNN\n",
      "Training:\n",
      "AUC:0.994\n",
      "accuracy:0.944\n",
      "recall:0.897\n",
      "precision:0.991\n",
      "specificity:0.991\n",
      "prevalence:0.500\n",
      " \n",
      "Validation:\n",
      "AUC:0.990\n",
      "accuracy:0.918\n",
      "recall:0.889\n",
      "precision:0.990\n",
      "specificity:0.980\n",
      "prevalence:0.684\n",
      " \n"
     ]
    }
   ],
   "source": [
    "y_train_preds = knn.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = knn.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "print('KNN')\n",
    "print('Training:')\n",
    "knn_train_auc, knn_train_accuracy, knn_train_recall, \\\n",
    "    knn_train_precision, knn_train_specificity = print_report(y_train,y_train_preds, thresh)\n",
    "print('Validation:')\n",
    "knn_valid_auc, knn_valid_accuracy, knn_valid_recall, \\\n",
    "    knn_valid_precision, knn_valid_specificity = print_report(y_valid,y_valid_preds, thresh)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "collapsed": true
   },
   "source": [
    "### Logistic Regression"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "It is statistics model which uses logistic function to model binary dependent variable. Like other analysis, Logistic Regression is a predictive examination. Logistic Regression is utilized to depict information and to clarify the connection between one ward parallel variable and at least one nominal, ordinal, interval or proportion level free factors. It is easy to implement and in training the model it is very efficient."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Training a logistic regression to evaluate the performance."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 913,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,\n",
       "          intercept_scaling=1, max_iter=100, multi_class='ovr', n_jobs=1,\n",
       "          penalty='l2', random_state=42, solver='liblinear', tol=0.0001,\n",
       "          verbose=0, warm_start=False)"
      ]
     },
     "execution_count": 913,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.linear_model import LogisticRegression\n",
    "lr=LogisticRegression(random_state = 42)\n",
    "lr.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 914,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Logistic Regression\n",
      "Training:\n",
      "AUC:1.000\n",
      "accuracy:0.996\n",
      "recall:0.991\n",
      "precision:1.000\n",
      "specificity:1.000\n",
      "prevalence:0.500\n",
      " \n",
      "Validation:\n",
      "AUC:1.000\n",
      "accuracy:0.981\n",
      "recall:0.972\n",
      "precision:1.000\n",
      "specificity:1.000\n",
      "prevalence:0.684\n",
      " \n"
     ]
    }
   ],
   "source": [
    "y_train_preds = lr.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = lr.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "print('Logistic Regression')\n",
    "print('Training:')\n",
    "lr_train_auc, lr_train_accuracy, lr_train_recall, \\\n",
    "    lr_train_precision, lr_train_specificity = print_report(y_train,y_train_preds, thresh)\n",
    "print('Validation:')\n",
    "lr_valid_auc, lr_valid_accuracy, lr_valid_recall, \\\n",
    "    lr_valid_precision, lr_valid_specificity = print_report(y_valid,y_valid_preds, thresh)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Stochastic Gradient Descent"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "It is an optimization method used for finding values of coefficients of a function to minimize the cost of function. Used when we cannot calculate the coefficients analytically and we need optimization for it. It is used when we have huge amount of data and Gradient Descent algorithm doesnâ€™t work or works slowly. In this variety, the gradient descent method depicted above is run yet the update to the coefficients is performed for each training instance, as opposed to toward the finish of the group of cases. Efficient, easy to imply for large scale machine learning problems."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Training a stochastic gradient descent model to evaluate the performance"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 915,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\sklearn\\linear_model\\stochastic_gradient.py:128: FutureWarning: max_iter and tol parameters have been added in <class 'sklearn.linear_model.stochastic_gradient.SGDClassifier'> in 0.19. If both are left unset, they default to max_iter=5 and tol=None. If tol is not None, max_iter defaults to max_iter=1000. From 0.21, default max_iter will be 1000, and default tol will be 1e-3.\n",
      "  \"and default tol will be 1e-3.\" % type(self), FutureWarning)\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "SGDClassifier(alpha=0.1, average=False, class_weight=None, epsilon=0.1,\n",
       "       eta0=0.0, fit_intercept=True, l1_ratio=0.15,\n",
       "       learning_rate='optimal', loss='log', max_iter=None, n_iter=None,\n",
       "       n_jobs=1, penalty='l2', power_t=0.5, random_state=42, shuffle=True,\n",
       "       tol=None, verbose=0, warm_start=False)"
      ]
     },
     "execution_count": 915,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# your code here\n",
    "from sklearn.linear_model import SGDClassifier\n",
    "sgdc=SGDClassifier(loss = 'log',alpha = 0.1,random_state = 42)\n",
    "sgdc.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 916,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Stochastic Gradient Descend\n",
      "Training:\n",
      "AUC:1.000\n",
      "accuracy:0.966\n",
      "recall:0.932\n",
      "precision:1.000\n",
      "specificity:1.000\n",
      "prevalence:0.500\n",
      " \n",
      "Validation:\n",
      "AUC:0.999\n",
      "accuracy:0.968\n",
      "recall:0.954\n",
      "precision:1.000\n",
      "specificity:1.000\n",
      "prevalence:0.684\n",
      " \n"
     ]
    }
   ],
   "source": [
    "y_train_preds = sgdc.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = sgdc.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "print('Stochastic Gradient Descend')\n",
    "print('Training:')\n",
    "sgdc_train_auc, sgdc_train_accuracy, sgdc_train_recall, sgdc_train_precision, sgdc_train_specificity =print_report(y_train,y_train_preds, thresh)\n",
    "print('Validation:')\n",
    "sgdc_valid_auc, sgdc_valid_accuracy, sgdc_valid_recall, sgdc_valid_precision, sgdc_valid_specificity = print_report(y_valid,y_valid_preds, thresh)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Naive Bayes"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "It is a supervised learning algorithm. It is based of application of Bayes theorem with the â€œnaiveâ€ assumption of conditional independence between every pair of features given the value of the class variable.  It is a classification method. It assumes independence in between predictors, which means that a feature is not dependent upon any other feature in a class. It is easy to build. Good to be used for large dataset. It always outperforms any high classification method. It performs well with categorial variables than the numerical ones."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Training Naive Bayes model and evaluating the performance."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 917,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "GaussianNB(priors=None)"
      ]
     },
     "execution_count": 917,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# your code here\n",
    "from sklearn.naive_bayes import GaussianNB\n",
    "\n",
    "nb = GaussianNB()\n",
    "nb.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 918,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Naive Bayes\n",
      "Training:\n",
      "AUC:0.995\n",
      "accuracy:0.675\n",
      "recall:1.000\n",
      "precision:0.606\n",
      "specificity:0.350\n",
      "prevalence:0.500\n",
      " \n",
      "Validation:\n",
      "AUC:0.991\n",
      "accuracy:0.785\n",
      "recall:1.000\n",
      "precision:0.761\n",
      "specificity:0.320\n",
      "prevalence:0.684\n",
      " \n"
     ]
    }
   ],
   "source": [
    "y_train_preds = nb.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = nb.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "print('Naive Bayes')\n",
    "print('Training:')\n",
    "nb_train_auc, nb_train_accuracy, nb_train_recall, nb_train_precision, nb_train_specificity =print_report(y_train,y_train_preds, thresh)\n",
    "print('Validation:')\n",
    "nb_valid_auc, nb_valid_accuracy, nb_valid_recall, nb_valid_precision, nb_valid_specificity = print_report(y_valid,y_valid_preds, thresh)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Decision Tree Classifier"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "It is classification algorithm which works on tree structure. Tree structure is basically a flow chart. Decision Tree Classifier is generally utilized arrangement method. It applies a thought to take care of the characterization issue. Decision Tree Classifier represents a progression of series of carefully crafted questions concerning the characteristics of the test record. Each time it gets an answer, a subsequent question is posed until a decision about the class name of the record is come to. The decision tree classifiers sorted out a progression of test questions and conditions in a tree structure."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Training Decision Tree model and evaluating the performance."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 919,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "DecisionTreeClassifier(class_weight=None, criterion='gini', max_depth=10,\n",
       "            max_features=None, max_leaf_nodes=None,\n",
       "            min_impurity_decrease=0.0, min_impurity_split=None,\n",
       "            min_samples_leaf=1, min_samples_split=2,\n",
       "            min_weight_fraction_leaf=0.0, presort=False, random_state=42,\n",
       "            splitter='best')"
      ]
     },
     "execution_count": 919,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# your code here\n",
    "from sklearn.tree import DecisionTreeClassifier\n",
    "\n",
    "tree = DecisionTreeClassifier(max_depth = 10, random_state = 42)\n",
    "tree.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 920,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Decision Tree\n",
      "Training:\n",
      "AUC:1.000\n",
      "accuracy:1.000\n",
      "recall:1.000\n",
      "precision:1.000\n",
      "specificity:1.000\n",
      "prevalence:0.500\n",
      " \n",
      "Validation:\n",
      "AUC:0.881\n",
      "accuracy:0.873\n",
      "recall:0.861\n",
      "precision:0.949\n",
      "specificity:0.900\n",
      "prevalence:0.684\n",
      " \n"
     ]
    }
   ],
   "source": [
    "y_train_preds = tree.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = tree.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "print('Decision Tree')\n",
    "print('Training:')\n",
    "tree_train_auc, tree_train_accuracy, tree_train_recall, tree_train_precision, tree_train_specificity =print_report(y_train,y_train_preds, thresh)\n",
    "print('Validation:')\n",
    "tree_valid_auc, tree_valid_accuracy, tree_valid_recall, tree_valid_precision, tree_valid_specificity = print_report(y_valid,y_valid_preds, thresh)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Random Forest"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "It is a supervised machine learning algorithm. It is easy to use and is flexible. Without using hyper parameter tuning it produces outputs. It is used for both classification and regression methods. It creates random forests which is obtained from merging of decision trees for more accurate and stable predictions. Random Forest adds extra arbitrariness to the model, while developing the trees. Rather than looking for the most significant component while part a node, it scans for the best element among a random subset of features. This outcomes in a wide assorted variety that by and large outcomes in a superior model. It uses only random subset of features to split the node."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Training Random Forest model and evaluating the performance"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 921,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "RandomForestClassifier(bootstrap=True, class_weight=None, criterion='gini',\n",
       "            max_depth=6, max_features='auto', max_leaf_nodes=None,\n",
       "            min_impurity_decrease=0.0, min_impurity_split=None,\n",
       "            min_samples_leaf=1, min_samples_split=2,\n",
       "            min_weight_fraction_leaf=0.0, n_estimators=10, n_jobs=1,\n",
       "            oob_score=False, random_state=42, verbose=0, warm_start=False)"
      ]
     },
     "execution_count": 921,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# your code here\n",
    "from sklearn.ensemble import RandomForestClassifier\n",
    "rf=RandomForestClassifier(max_depth = 6, random_state = 42)\n",
    "rf.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 922,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Random Forest\n",
      "Training:\n",
      "AUC:0.999\n",
      "accuracy:0.989\n",
      "recall:0.983\n",
      "precision:0.996\n",
      "specificity:0.996\n",
      "prevalence:0.500\n",
      " \n",
      "Validation:\n",
      "AUC:0.984\n",
      "accuracy:0.918\n",
      "recall:0.917\n",
      "precision:0.961\n",
      "specificity:0.920\n",
      "prevalence:0.684\n",
      " \n"
     ]
    }
   ],
   "source": [
    "y_train_preds = rf.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = rf.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "print('Random Forest')\n",
    "print('Training:')\n",
    "rf_train_auc, rf_train_accuracy, rf_train_recall, rf_train_precision, rf_train_specificity =print_report(y_train,y_train_preds, thresh)\n",
    "print('Validation:')\n",
    "rf_valid_auc, rf_valid_accuracy, rf_valid_recall, rf_valid_precision, rf_valid_specificity = print_report(y_valid,y_valid_preds, thresh)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Gradient Boosting Classifier"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "It gives a prediction model in the form of an ensemble of decision trees. It is used for both classification as well as regression methods. It is boosting method in which each new tree is fit on a modified version of original data set. It trains models in a gradual, additive and sequential manner. The gradient boosting model identifies the defects by using gradients in the loss function. A loss function depends on what we are trying to optimize, and it is a measure to know good the model coefficients are fitting the data. It enables one to improve a client indicated cost work, rather than a loss that normally offers less control and does not basically relate with certifiable applications. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Training Gradient Boosting model and evaluating the performance."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 923,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "GradientBoostingClassifier(criterion='friedman_mse', init=None,\n",
       "              learning_rate=1.0, loss='deviance', max_depth=3,\n",
       "              max_features=None, max_leaf_nodes=None,\n",
       "              min_impurity_decrease=0.0, min_impurity_split=None,\n",
       "              min_samples_leaf=1, min_samples_split=2,\n",
       "              min_weight_fraction_leaf=0.0, n_estimators=100,\n",
       "              presort='auto', random_state=42, subsample=1.0, verbose=0,\n",
       "              warm_start=False)"
      ]
     },
     "execution_count": 923,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# your  code here\n",
    "from sklearn.ensemble import GradientBoostingClassifier\n",
    "gbc =GradientBoostingClassifier(n_estimators=100, learning_rate=1.0,\n",
    "     max_depth=3, random_state=42)\n",
    "gbc.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 924,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Gradient Boosting Classifier\n",
      "Training:\n",
      "AUC:1.000\n",
      "accuracy:1.000\n",
      "recall:1.000\n",
      "precision:1.000\n",
      "specificity:1.000\n",
      "prevalence:0.500\n",
      " \n",
      "Validation:\n",
      "AUC:0.991\n",
      "accuracy:0.956\n",
      "recall:0.954\n",
      "precision:0.981\n",
      "specificity:0.960\n",
      "prevalence:0.684\n",
      " \n"
     ]
    }
   ],
   "source": [
    "y_train_preds = gbc.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = gbc.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "print('Gradient Boosting Classifier')\n",
    "print('Training:')\n",
    "gbc_train_auc, gbc_train_accuracy, gbc_train_recall, gbc_train_precision, gbc_train_specificity = print_report(y_train,y_train_preds, thresh)\n",
    "print('Validation:')\n",
    "gbc_valid_auc, gbc_valid_accuracy, gbc_valid_recall, gbc_valid_precision, gbc_valid_specificity = print_report(y_valid,y_valid_preds, thresh)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Analyze results baseline models"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Let's make a dataframe with these results and plot the outcomes using a package called seaborn."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 925,
   "metadata": {},
   "outputs": [],
   "source": [
    "df_results = pd.DataFrame({'classifier':['KNN','KNN','LR','LR','SGD','SGD','NB','NB','DT','DT','RF','RF','GB','GB'],\n",
    "                           'data_set':['train','valid']*7,\n",
    "                          'auc':[knn_train_auc, knn_valid_auc,lr_train_auc,lr_valid_auc,sgdc_train_auc,sgdc_valid_auc,nb_train_auc,nb_valid_auc,tree_train_auc,tree_valid_auc,rf_train_auc,rf_valid_auc,gbc_train_auc,gbc_valid_auc,],\n",
    "                          'accuracy':[knn_train_accuracy, knn_valid_accuracy,lr_train_accuracy,lr_valid_accuracy,sgdc_train_accuracy,sgdc_valid_accuracy,nb_train_accuracy,nb_valid_accuracy,tree_train_accuracy,tree_valid_accuracy,rf_train_accuracy,rf_valid_accuracy,gbc_train_accuracy,gbc_valid_accuracy,],\n",
    "                          'recall':[knn_train_recall, knn_valid_recall,lr_train_recall,lr_valid_recall,sgdc_train_recall,sgdc_valid_recall,nb_train_recall,nb_valid_recall,tree_train_recall,tree_valid_recall,rf_train_recall,rf_valid_recall,gbc_train_recall,gbc_valid_recall,],\n",
    "                          'precision':[knn_train_precision, knn_valid_precision,lr_train_precision,lr_valid_precision,sgdc_train_precision,sgdc_valid_precision,nb_train_precision,nb_valid_precision,tree_train_precision,tree_valid_precision,rf_train_precision,rf_valid_precision,gbc_train_precision,gbc_valid_precision,],\n",
    "                          'specificity':[knn_train_specificity, knn_valid_specificity,lr_train_specificity,lr_valid_specificity,sgdc_train_specificity,sgdc_valid_specificity,nb_train_specificity,nb_valid_specificity,tree_train_specificity,tree_valid_specificity,rf_train_specificity,rf_valid_specificity,gbc_train_specificity,gbc_valid_specificity,]})"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 926,
   "metadata": {},
   "outputs": [],
   "source": [
    "import seaborn as sns\n",
    "import matplotlib.pyplot as plt\n",
    "sns.set(style=\"darkgrid\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 3: Pick one performance metric that you will use for picking the best model. Explain your choice of performance metric. Make a bar plot of this performance metric below to demonstrate the baseline performance. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "I am picking Random Forest as my Area under the curve and recall factor of test and validation data are giving best results."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 927,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "# Your code here\n",
    "ax = sns.barplot(x=\"classifier\", y=\"auc\", hue=\"data_set\", data=df_results)\n",
    "ax.set_xlabel('Classifier',fontsize = 15)\n",
    "ax.set_ylabel('AUC', fontsize = 15)\n",
    "ax.tick_params(labelsize=15)\n",
    "\n",
    "# Put the legend out of the figure\n",
    "plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0., fontsize = 15)\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 928,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "image/png": "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Zcuwb98+5OTk4NSpU/jxxx+xdu1adO7cGVOnTsWWLVswbNgw7Ny5s8b1t2nTBteuXUOrVq00/y5evIiVK1e+8GdDROLAYXYilA2J//jjjwgKCsLMmTPh7OyMW7duISkpCf/973+RlJSkdTV7kyZNoK+vjwMHDsDc3Bz5+flYuXIlFAoFFAoF9PX1cebMGaSlpSEiIgKWlpbYs2cPDAwM0LFjR9y8eRNr166FmZkZevTogVu3buHkyZNwcXGpce3vvvsuJk2ahHbt2sHPzw/Xrl1DZGQkunfvzgvdiBoJhjkRyu7rTklJwfr167FmzRrcuHEDZmZmcHZ2xtatW/H3v/9d62p2W1tbLF26FPHx8fjss89ga2sLf39/2Nraap4YFxsbi6VLl2LSpEkoLCxE27ZtsXbtWs3R89KlS7FhwwasWLECpqam6N27N957770a1/76668jJiYG69atw0cffQRLS0sEBARg5syZtfb5EFHDxifAERERiRzPmRMREYkcw5yIiEjkGOZEREQixzAnIiISOYY5ERGRyDHMiYiIRI5hTkREJHIMcyIiIpFjmBMREYnc/wMCFrBZSoB8JwAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "ax = sns.barplot(x=\"classifier\", y=\"recall\", hue=\"data_set\", data=df_results)\n",
    "ax.set_xlabel('Classifier',fontsize = 15)\n",
    "ax.set_ylabel('recall', fontsize = 15)\n",
    "ax.tick_params(labelsize=15)\n",
    "\n",
    "# Put the legend out of the figure\n",
    "plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0., fontsize = 15)\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 929,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "ax = sns.barplot(x=\"classifier\", y=\"specificity\", hue=\"data_set\", data=df_results)\n",
    "ax.set_xlabel('Classifier',fontsize = 15)\n",
    "ax.set_ylabel('specificity', fontsize = 15)\n",
    "ax.tick_params(labelsize=15)\n",
    "\n",
    "# Put the legend out of the figure\n",
    "plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0., fontsize = 15)\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 930,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "ax = sns.barplot(x=\"classifier\", y=\"precision\", hue=\"data_set\", data=df_results)\n",
    "ax.set_xlabel('Classifier',fontsize = 15)\n",
    "ax.set_ylabel('precision', fontsize = 15)\n",
    "ax.tick_params(labelsize=15)\n",
    "\n",
    "# Put the legend out of the figure\n",
    "plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0., fontsize = 15)\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 931,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "ax = sns.barplot(x=\"classifier\", y=\"accuracy\", hue=\"data_set\", data=df_results)\n",
    "ax.set_xlabel('Classifier',fontsize = 15)\n",
    "ax.set_ylabel('accuracy', fontsize = 15)\n",
    "ax.tick_params(labelsize=15)\n",
    "\n",
    "# Put the legend out of the figure\n",
    "plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0., fontsize = 15)\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "My current best model is: Logistic Regression model"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 932,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "5 0.01793980598449707\n",
      "10 0.01396322250366211\n",
      "15 0.010970592498779297\n",
      "20 0.012965917587280273\n",
      "25 0.011967658996582031\n",
      "30 0.011968374252319336\n"
     ]
    }
   ],
   "source": [
    "import time\n",
    "\n",
    "my_params = [5,10,15,20,25,30] # your list of parameters\n",
    "\n",
    "# initialize arrays for storing the results\n",
    "train_aucs = np.zeros(len(my_params))\n",
    "valid_aucs = np.zeros(len(my_params))\n",
    "\n",
    "# train a model for each K in a list. Store the auc for the training and validation set\n",
    "t1 = time.time()\n",
    "for jj in range(len(my_params)):\n",
    "    my_param = my_params[jj]\n",
    "    \n",
    "    # fit model\n",
    "    model = RandomForestClassifier(max_depth = my_param, random_state = 42)\n",
    "    model.fit(X_train_tf, y_train)\n",
    "    # get predictions\n",
    "    y_train_preds = model.predict_proba(X_train_tf)[:,1]\n",
    "    y_valid_preds = model.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "    # calculate auc\n",
    "    auc_train = roc_auc_score(y_train, y_train_preds)\n",
    "    auc_valid = roc_auc_score(y_valid, y_valid_preds)\n",
    "\n",
    "    # save aucs\n",
    "    train_aucs[jj] = auc_train\n",
    "    valid_aucs[jj] = auc_valid\n",
    "    \n",
    "    # print the time\n",
    "    t2 = time.time()\n",
    "    print(my_param, t2-t1)\n",
    "    t1 = time.time()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 933,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAZYAAAEXCAYAAACOFGLrAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAIABJREFUeJzt3XlYVHX///HnDDMoKIQLi5alueGC0uKaYVQ3IIsoqblbuLTdmaYVlraAuWU3ZVm/vmW5pIU7okKK3dptcntHZViBuWFu7CqrwMw5vz/IKVIUcIYB5v24rq6rc86cc97vGeTFWeZzNKqqqgghhBBmorV2AUIIIRoXCRYhhBBmJcEihBDCrCRYhBBCmJUEixBCCLOSYBFCCGFWEizCYrp27UpISAihoaGV/jtz5gwAr732Gg8++CDR0dHs378fX19fRowYweXLl2u8r7179/Luu+/WaB2j0chTTz2Fv78/n3/+eaVl7733Hl27dmXTpk2V5hcXF3PXXXfxxBNP1LjGqjz44IP4+/sTGhrK0KFDCQkJ4cMPP8RgMNzUdt9//30SExMBiIiIYMWKFeYot9qeffZZ+vXrR0lJSaX5EyZMICEhodK8vLw8unbtapo2Go189tlnhIWFERoaSmBgIG+99RZlZWV1Uru4OTprFyAat1WrVtGyZctrLouJiWHv3r14eHgwZ84cRo4cydNPP12r/Rw+fJhLly7VaJ3MzEz279/PoUOHsLOzu2p527ZtiY2N5ZFHHjHN27VrF46OjrWq8XqWLl2Kl5cXUBFes2fPZuHChcybN6/W2zx48CCdOnUyV4k1kpmZyXfffYe3tzdbt25lzJgxNVr/9ddf59KlS6xatQonJyfTe/LKK6/w1ltvWahqYS4SLMIqxo4di6qqTJ06lYCAAPbs2UOTJk0oKCjgpZde4sMPP2TXrl0oisKtt97Ka6+9hru7O9nZ2bz22mucOHECrVbL6NGj6d27N19++SVGoxEnJydmzpxZaV/JycksWbKEkpIS9Ho9M2bM4O6772bKlCkYDAbCwsJ47733uP322yutd//995OYmEhGRgYeHh4AbNmyhaFDh3LixAkATp48SWRkJEVFRWRnZ+Pp6ck777zDmTNnGD16NKtXr6Zbt268+OKL6HQ6FixYcMP3xtHRkVdffZWHH36YmTNn0rx5czZs2MAXX3yBoii4uLgwb948OnbsSEREBE2aNCEtLY3c3Fzuu+8+5s6dy/r16/n5559ZsmSJKTR//PFHRo8eTU5ODp07d+btt9++KiQLCgp44403SEtLQ6PRcP/99/P888+j0+nw8vJi2rRpfPvtt2RlZTFlyhTGjh17zR7Wr1/PgAED8Pf3591332X06NFoNJpq/WycOXOGuLg49u/fT/PmzU3vyRtvvMEPP/xQrW0IK1OFsJAuXbqowcHB6tChQ03/Pf3005WW5+bmqqqqqi+99JL6ySefqKqqqlu2bFFnzJihlpeXq6qqql9++aU6ZcoUVVVV9ZlnnlEXL16sqqqq5ufnq0FBQWp6erq6bNky9Y033riqhry8PHXAgAHqoUOHVFVV1d9++03t27ev+vvvv6unT59Wvb29r1n7le1FRkaqH330kaqqqnr27Fn1kUceUTdt2qROmzZNVVVVXbRokbp161ZVVVW1rKxMDQ4OVhMSElRVVdWYmBg1JCREXb9+vRoSEqKWlJRcc1++vr5qSkrKVfP79eun/vTTT+rBgwfVsWPHqsXFxaqqqup//vMfNSAgwPS+DRs2TC0sLFRLS0vVcePGqWvWrFFVVVXHjx+vxsfHm143YsQItbi4WDUYDOrw4cPVLVu2XLXPF198UY2KilIVRVFLS0vV8PBwU/9dunQxbfvw4cNqz5491cuXL1+1jfLycnXQoEHq119/rZaWlqp9+vRR9+7da1r+17quyM3NVbt06aKqqqomJCSojzzyyDXfK9EwyBGLsKjrnQqryr///W8OHz5sOgWlKIrpPP2BAwd44YUXAHBycmL79u3X3VZKSgq33347vXv3BqBz587cfffd/O9//6Nfv343rCU0NJRXXnmFadOmERsby7Bhwyotf+GFF/j222/5+OOPSU9PJysri+LiYgBGjRrF/v37mT9/PrGxsTRt2rRG74NGo8HBwYGEhAROnTrF6NGjTcvy8/O5ePEiAMOHD6dZs2amevfs2cP48eOv2t7DDz+Mg4OD6X3Iy8u76jXffPMNX3zxBRqNBnt7e0aPHs2qVauYNm0aAA899BAAPXr0oKysjOLiYpo0aVJpG3v27EFRFO6//350Oh2BgYGsXr2awYMHm/r6O1VV0WorLvlqtVoURanReyXqFwkWUe8oilLpNEtZWZnp+olO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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "import matplotlib.pyplot as plt\n",
    "\n",
    "plt.plot(my_params, train_aucs,'o-',label = 'train')\n",
    "plt.plot(my_params, valid_aucs,'o-',label = 'valid')\n",
    "\n",
    "plt.xlabel('Max-Depth') # fill this in\n",
    "plt.ylabel('AUC')# fill this in\n",
    "plt.title('Effect of Max-Depth on AUC') # fill this in\n",
    "plt.legend()\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Learning Curves"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 4: Using your baseline model that has the best performance on the validation set, plot a learning curve for that model. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 934,
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "from sklearn.model_selection import learning_curve\n",
    "from sklearn.model_selection import ShuffleSplit\n",
    "\n",
    "def plot_learning_curve(estimator, title, X, y, ylim=None, cv=None,\n",
    "                        n_jobs=1, train_sizes=np.linspace(.1, 1.0, 5)):\n",
    "    \"\"\"\n",
    "    Generate a simple plot of the test and training learning curve.\n",
    "\n",
    "    Parameters\n",
    "    ----------\n",
    "    estimator : object type that implements the \"fit\" and \"predict\" methods\n",
    "        An object of that type which is cloned for each validation.\n",
    "\n",
    "    title : string\n",
    "        Title for the chart.\n",
    "\n",
    "    X : array-like, shape (n_samples, n_features)\n",
    "        Training vector, where n_samples is the number of samples and\n",
    "        n_features is the number of features.\n",
    "\n",
    "    y : array-like, shape (n_samples) or (n_samples, n_features), optional\n",
    "        Target relative to X for classification or regression;\n",
    "        None for unsupervised learning.\n",
    "\n",
    "    ylim : tuple, shape (ymin, ymax), optional\n",
    "        Defines minimum and maximum yvalues plotted.\n",
    "\n",
    "    cv : int, cross-validation generator or an iterable, optional\n",
    "        Determines the cross-validation splitting strategy.\n",
    "        Possible inputs for cv are:\n",
    "          - None, to use the default 3-fold cross-validation,\n",
    "          - integer, to specify the number of folds.\n",
    "          - An object to be used as a cross-validation generator.\n",
    "          - An iterable yielding train/test splits.\n",
    "\n",
    "        For integer/None inputs, if ``y`` is binary or multiclass,\n",
    "        :class:`StratifiedKFold` used. If the estimator is not a classifier\n",
    "        or if ``y`` is neither binary nor multiclass, :class:`KFold` is used.\n",
    "\n",
    "        Refer :ref:`User Guide <cross_validation>` for the various\n",
    "        cross-validators that can be used here.\n",
    "\n",
    "    n_jobs : integer, optional\n",
    "        Number of jobs to run in parallel (default 1).\n",
    "    \"\"\"\n",
    "    plt.figure()\n",
    "    plt.title(title)\n",
    "    if ylim is not None:\n",
    "        plt.ylim(*ylim)\n",
    "    plt.xlabel(\"Training examples\")\n",
    "    plt.ylabel(\"AUC\")\n",
    "    train_sizes, train_scores, test_scores = learning_curve(\n",
    "        estimator, X, y, cv=cv, n_jobs=n_jobs, train_sizes=train_sizes, scoring = 'roc_auc')\n",
    "    train_scores_mean = np.mean(train_scores, axis=1)\n",
    "    train_scores_std = np.std(train_scores, axis=1)\n",
    "    test_scores_mean = np.mean(test_scores, axis=1)\n",
    "    test_scores_std = np.std(test_scores, axis=1)\n",
    "    plt.grid()\n",
    "\n",
    "    plt.fill_between(train_sizes, train_scores_mean - train_scores_std,\n",
    "                     train_scores_mean + train_scores_std, alpha=0.1,\n",
    "                     color=\"r\")\n",
    "    plt.fill_between(train_sizes, test_scores_mean - test_scores_std,\n",
    "                     test_scores_mean + test_scores_std, alpha=0.1, color=\"b\")\n",
    "    plt.plot(train_sizes, train_scores_mean, 'o-', color=\"r\",\n",
    "             label=\"Training score\")\n",
    "    plt.plot(train_sizes, test_scores_mean, 'o-', color=\"b\",\n",
    "             label=\"Cross-validation score\")\n",
    "\n",
    "    plt.legend(loc=\"best\")\n",
    "    return plt"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 935,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "# Cross validation with 5 iterations to get smoother mean test and train\n",
    "# score curves, each time with 20% data randomly selected as a validation set.\n",
    "\n",
    "\n",
    "title = \"Learning Curves (Random Forest)\"                                        # fill this in\n",
    "cv = ShuffleSplit(n_splits=5, test_size=0.2, random_state=42)\n",
    "estimator = RandomForestClassifier(max_depth = 5, random_state = 42)                                  # fill this in\n",
    "plot_learning_curve(estimator, title, X_train_tf, y_train, ylim=(0.2, 1.01), cv=cv, n_jobs=4)\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "My best perfomance model of Random Forest classifier is high bias which is also known as underfitting. It means that the model is not capturing all the signals as it would from data. It is a measure of model rigidity and inflexibility.\n",
    "To improve this model the techniques we can use is to add more features, Regularization,Change model architecture."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Feature Importance"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 4: Plot the feature importance for logistic regression and random forest models here. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 936,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,\n",
       "          intercept_scaling=1, max_iter=100, multi_class='ovr', n_jobs=1,\n",
       "          penalty='l2', random_state=42, solver='liblinear', tol=0.0001,\n",
       "          verbose=0, warm_start=False)"
      ]
     },
     "execution_count": 936,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Your code here\n",
    "from sklearn.linear_model import LogisticRegression\n",
    "lr=LogisticRegression(random_state = 42)\n",
    "lr.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 937,
   "metadata": {},
   "outputs": [],
   "source": [
    "feature_importances = pd.DataFrame(lr.coef_[0],\n",
    "                                   index = cols_input,\n",
    "                                    columns=['importance']).sort_values('importance',\n",
    "                                                                        ascending=False)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 938,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>importance</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>A9</th>\n",
       "      <td>1.599175</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A2</th>\n",
       "      <td>1.523437</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A6</th>\n",
       "      <td>1.411448</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A8</th>\n",
       "      <td>1.354897</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A4</th>\n",
       "      <td>1.304955</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A7</th>\n",
       "      <td>1.241910</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A5</th>\n",
       "      <td>1.233738</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A10</th>\n",
       "      <td>1.223835</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A1</th>\n",
       "      <td>1.094651</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A3</th>\n",
       "      <td>1.011559</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Age_Mons</th>\n",
       "      <td>0.257108</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Jaundice_yes</th>\n",
       "      <td>0.239848</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Family_mem_with_ASD_yes</th>\n",
       "      <td>0.148071</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Sex_m</th>\n",
       "      <td>0.051967</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Who completed the test_family member</th>\n",
       "      <td>-0.019022</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Who completed the test_Others</th>\n",
       "      <td>-0.194593</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Who completed the test_Self</th>\n",
       "      <td>-0.274428</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Who completed the test_Health care professional</th>\n",
       "      <td>-0.279924</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                                                 importance\n",
       "A9                                                 1.599175\n",
       "A2                                                 1.523437\n",
       "A6                                                 1.411448\n",
       "A8                                                 1.354897\n",
       "A4                                                 1.304955\n",
       "A7                                                 1.241910\n",
       "A5                                                 1.233738\n",
       "A10                                                1.223835\n",
       "A1                                                 1.094651\n",
       "A3                                                 1.011559\n",
       "Age_Mons                                           0.257108\n",
       "Jaundice_yes                                       0.239848\n",
       "Family_mem_with_ASD_yes                            0.148071\n",
       "Sex_m                                              0.051967\n",
       "Who completed the test_family member              -0.019022\n",
       "Who completed the test_Others                     -0.194593\n",
       "Who completed the test_Self                       -0.274428\n",
       "Who completed the test_Health care professional   -0.279924"
      ]
     },
     "execution_count": 938,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "feature_importances"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 939,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>importance</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>A9</th>\n",
       "      <td>1.599175</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A2</th>\n",
       "      <td>1.523437</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A6</th>\n",
       "      <td>1.411448</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A8</th>\n",
       "      <td>1.354897</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A4</th>\n",
       "      <td>1.304955</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "    importance\n",
       "A9    1.599175\n",
       "A2    1.523437\n",
       "A6    1.411448\n",
       "A8    1.354897\n",
       "A4    1.304955"
      ]
     },
     "execution_count": 939,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "feature_importances.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 940,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAArwAAAPRCAYAAAAfp3tzAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAMTQAADE0B0s6tTgAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAIABJREFUeJzs3Xl4VOX9///XJENWIgQS0YioVUkFC5KAEYIfYiQNGEaNgQp1a92KKO6KuAAiUhGo1rogUqUqtaCQQFJARWvdTcVEtGKsuLCELauQbTLJ/f2DH/MjgpiETGZy5/m4rrku5uScM+/3zJnJizv3meMwxhgBAAAAlgrydwEAAACALxF4AQAAYDUCLwAAAKxG4AUAAIDVCLwAAACwGoEXAAAAViPwAugQamtrtWvXLn+X0Wrff/+9v0tod52xZ1vt2LFDbrfb32UArUbgBXBE4uPjNXDgQA0aNEiDBg1SQkKCLrnkEn388cdHtN/i4mINGjRI5eXlkqTf/va3+uSTTyRJq1at0tixY4+49gOtWLFCp512mrePA29H6o033tANN9zQBlX+vBUrVmjMmDHt8liH88UXX2jcuHH+LqOJsrIy3XvvvRo+fLjOOOMMpaamas6cOaqtrfV3aYe1detWxcfHq6ysrM33PWjQIH3xxReHXaekpESjR4/W3r17JUnTpk3TQw891KLH2d/Dge+r/a/BwoULW11/e7v66qv1/PPP+7sMtILT3wUA6PhefPFF/epXv5IkNTY26vnnn9e1116rf/3rX+rWrVur9hkXF6eCggLv/YqKCu+/zz//fJ1//vlHVvQhnHzyycrLy2vz/VZWVqqzXeNnz549qq+v93cZTdx666065phjlJeXp+7du2vz5s26/fbbNW3aND388MP+Ls8vDnyP/ZTa2lpVV1d778+cObPVj/fGG2+oR48ekvZ9Vrz33nuaNGmS+vfvr+Tk5Fbvt70sWrTI3yWglRjhBdCmgoKC9Jvf/EZVVVXavHmzJOmDDz7QuHHjlJCQoFGjRmnp0qXe9d98801lZGRo8ODBcrlcWr58uaSmo1oTJ05UcXGx7rzzTj3xxBPeUczGxkalpKRo7dq13v1t27ZNp59+ukpKSlRXV6c5c+YoJSVFw4YN01133aUffvih1b29/PLLGjVqlIYMGaIrrrhCmzZt8v7stdde09ixY5WUlKTExETdcsstqqmpUUFBgaZPn65NmzZp0KBBamhoUGpqapOa//rXv+qyyy6TtG+Edvz48ZowYYLOPPNMFRYWqrKyUlOnTtXw4cN19tln649//GOz/ry8detWDRo0SEuWLNHw4cOVmJioxx9/XHl5eUpNTVViYqJmzZrlXT81NVWPP/64UlNTlZCQoBtvvFGVlZXeny9ZskS//vWvlZiYqIsvvrjJKH58fLweeOABnXnmmZo6daquueYaVVdXa9CgQdqyZYt27NihG264QSkpKRowYIAuvPBC74j9Rx99pIyMDM2bN09nnXWWkpOTm4wg7tq1S5MnT1ZiYqKGDRumOXPmqLGxUZL0ySefaPz48d7j58033/zJ56OgoECjRo1S9+7dJUl9+vTRPffco+jo6CbrXHzxxRo0aJDS0tKUk5PT4v5nz54t6fDHS1sqLS3VlClTNHToUCUnJ2vq1KlN/oO4YMECDR8+XMOHD9f8+fOVmpqqjz76yFv3Z5995l1vxIgRSkpK0oQJE/Tpp59Kki644AJJ0rnnnquPPvpId911lzf0ut1uzZkzR8nJyRoyZIiuv/76Zo9EBwUF6eyzz9app56qL7/8UpLU0NCghQsXauTIkUpKStKkSZO0c+dO7zYvv/yyUlNTlZSUpHvvvVfjx4/XihUrJO07fqdNm6azzjpLkydPlrTv8+WCCy7Q4MGDNW7cOO8xd7h+y8rKdO211+rMM89USkqK7rrrLtXU1EiSLrvsMv31r3+VJFVXV2vWrFkaPny4kpKSdMMNN6i4uFjSzx/T8AMDAEegb9++ZsOGDd77e/bsMY8++qhJTk421dXV5uuvvzann366yc7ONvX19aawsNAkJSWZvLw84/F4TGJiovnggw+MMca8++67ZuDAgaasrMxs2bLF9O3b15SWlhpjjDnnnHPMmjVrjDHGLF++3GRkZBhjjPnTn/5kJk2a5H38J5980vzhD38wxhjzwAMPmAkTJphdu3aZPXv2mFtvvdVMnjz5kH0cuM9DefXVV82wYcPM559/btxut/nb3/5mRowYYaqrq01xcbEZMGCAyc/PN8YYs2XLFjN8+HCzbNmyQ+77wF6MMWbRokXm0ksv9a7bt29f8/rrr5u9e/caj8dj/vCHP5jJkyebH374wZSWlprLL7/cPPTQQz/bx/7n8O677zZ1dXXmnXfeMX379jXXXXed2bt3r/nvf/9r+vXrZz777DNvXSNHjjTfffedqaioMJdffrm55ZZbjDHGLFu2zAwdOtR8+umnpr6+3ixfvtwMHDjQbN682Xsc3Hzzzaa2ttb88MMP5sMPPzRnnHGGt66rrrrKzJw509TV1Zna2lozdepUM2HCBGOMMR9++KHp27evmT9/vnG73SY/P9/069fPfPLJJ8YYYy6++GJz2223mT179pidO3ea9PR08+KLL5ri4mJzxhlnmFWrVhmPx2M+/PBDM3jwYLNx48ZDPjd33nmnSUpKMg8++KB5/fXXTUlJSZOfl5aWmsTERPPCCy+Y+vp6s379ejNgwADz5Zdftrj/wx0vLfXj98KPTZgwwUyaNMlUVFSYiooKM3HiRHPVVVcZY4zJzs42ycnJpqioyNTU1Jh77rnH9O3b13z44Yfeujds2GA+++wzM2zYMLNz507T0NBgHn30UTNu3LhDPv6UKVPM/fffb4zZ9/5zuVxmy5Ytpra21tx0002HfI8dqge3221WrVplTj/9dO8x+Oyzz5pRo0aZ7777ztTW1po5c+aYrKws09jYaPLz880ZZ5xh/vOf/5i6ujrzl7/8xfTt29csX77cGLPv+J0wYYLZu3ev+eGHH8yGDRvMGWecYd5//31TX19v1qxZYwYPHmx27tx52H5nzpxppk6daurr6015eblxuVxmyZIlxhhjLr30UrNo0SJjjDG33367ufjii82OHTtMdXW1ue+++8yYMWOM2+3+2WMa7Y8RXgBH7PLLL9fgwYM1ePBgjRw5Up9++qmeeuophYeHKy8vT4mJibrwwgvldDo1cOBAXXbZZVq+fLmCg4MVFRWlFStWKD8/X2eeeaY++eSTJiNuPyczM1Nvv/22d+R21apVyszMlDFGL7/8sm6//XbFxsaqa9euuuuuu/Tqq6/+5AjUpk2bvH3sv7311luSpGXLlumyyy5T//791aVLF11++eUKCwvTv//9b/Xs2VN5eXkaMmSIKisrVVJSoujo6CYjUy1x1FFHaeTIkYqMjFR5ebn+9a9/6Z577lFUVJR69OihW265Rf/4xz+avb8rr7xSISEhGjp0qCTp0ksvVWRkpPr166fY2FjvqJQkXXvttTrhhBPUrVs33XzzzXrttddUV1ennJwcXXrppRowYICcTqcuuugiDRw4UP/85z+922ZkZCg0NFRRUVEH1TBr1izdfvvtkvaNwh911FEHPT8TJ05Uly5dNGTIEPXu3Vvff/+9tm7dqoKCAk2ZMkVdu3bV0UcfraefflrnnnuucnNzNWjQILlcLgUHByspKUmjR4/WsmXLDvk8zJ49W3fccYc2bdqkO+64Q8OGDdPFF1/sHdl76623FBMTo0svvVROp1MJCQl66aWXFBcX1+L+D3e8tKUtW7Zo/fr1uu+++9StWzd169ZN06ZN0zvvvKOdO3cqJydHl112mfr27auwsDBNnTpVwcHBB+2na9eu2rNnj5YtW6avvvpKkydP/snn8UC5ubn6wx/+oN69eys0NFTTpk077Hz1tLQ0DR48WAMGDNAZZ5yhVatWacGCBTr99NMl7XufTZo0SSeccIJCQ0N16623atOmTfr888+Vk5Mjl8ulwYMHKyQkRJMmTdLRRx/dZP/p6emKjIxUVFSUXnnlFY0ZM0ZDhw6V0+nUqFGjNGDAAOXm5h6236OOOkoFBQVavXq1GhsblZOTo9/+9rdNHqeurk5r1qzR7bffrl69eik8PFz33HOPtmzZ4h0xlw59TMM/mMML4Ig9//zz3jm8P1ZaWqrjjjuuybLevXsrNzdXkvTss8/q8ccf1+TJk1VfX69x48bptttua/Zjn3jiierfv79effVV/fKXv1RZWZnOOecclZWVqba2Vtdcc40cDod3/dDQUG3dutU7j/BAh5vDW1xcrAULFjSZw+fxeFRcXKwuXbpoxYoVevnllxUaGqp+/fqptra21fN2D/wlvj+MZmRkNFnH4/GotLRUPXv2/Nn97f8PxP6gc2AgDQoK8k4PkKQTTjjB++9jjz1W9fX13hB/qNfxwLD84/BxoG+//VZz585VcXGxTjnlFEVGRjZ5fiIiIhQREeG936VLFzU2NqqkpEROp1OxsbEH1VhcXKz8/HwNHjzY+7OGhgadddZZh6whODhYWVlZysrKksfj0caNG7V48WJdeeWVevPNN1VSUqJjjz22yTb9+vWTpBb3f7jj5ccyMjK8yxMTE1s0T3T/83PMMcd4lx177LFyOp3avn27duzY0aSnyMjIQ/6H8sQTT9QTTzyhxYsX65lnnlH37t11ww03/OyJh7t3727y2D169Djke2u/119/XT169NDWrVt18803KzQ0VElJSd6fFxcXa9q0abr//vu9yxobG7Vt2zbt2LGjyWsdFBR00Ov149fgo48+0po1a7zLGhoadNJJJx2230mTJik4OFgLFy7UlClTlJiYqPvvv18nn3yydz+VlZWqr69X7969vctCQ0MVGxur7du3KyYm5iePafgHgReATx177LH68MMPmyzbsmWLYmNjVV1dre3bt2v+/PkyxqigoEA33HCD4uPjdeaZZzb7MS666CKtXr1aX3/9tcaMGaOQkBBFR0crJCRE//jHP3TqqadK2hc4vv/++yahrrl69eqlSy65RJdccol32XfffafY2Fjl5eUpJydHr7zyiveX//jx439yX0FBQU1O6DpwvqWkJgG9V69ecjgceuutt9S1a1dJUk1NjXbt2nXYYNFaB466btu2TWFhYYqOjlZcXJy2bt3aZN3Nmzc3eZ0OrPtAbrdbkyZN0owZM7zzQZcuXar//e9/P1vPMcccI4/Ho5KSEsXExEiS3nnnHZWWlqpXr15KTU3VY4895l1/x44dCgkJOWg/b7/9tm699Vb9+9//VmRkpJxOp371q19pzpw5GjBggL7//nv16tVLO3bsaLLdkiVLdNppp7W4/8MdLz924ChxS8XFxcnj8Wj79u3e8Ldt2zZ5PB7FxMTo2GOPbdJTbW3tQcebtO9179atm/7617+qrq5Oa9eu1Z133qmzzjrrJ19Xad/rc+Axs2XLFi1fvlw333zzYevu3bu3nnrqKV1wwQWaNWuWZsyYIWnf83b33XcrJSXFu+6mTZvUu3dvvfvuu9q+fbt3uTHmoL8SHOo1mDJlSpP6unXrdth+KyoqNG7cON1www3auXOnZs+erRkzZuiFF17w7icmJkYhISHaunWr9z2//6sT9x+nCCxMaQDgU2PGjFFhYaFycnLk8Xj06aef6sUXX9SFF16ohoYGTZo0SatWrZK0b3TG4XB4Tyo6UEhIiPbs2XPIxzjvvPP02Wef6Z///KcyMzMl7QuVmZmZmjt3rsrKyuR2u/Xoo4/q8ssvl8fjaXEfWVlZeu655/TVV1/JGKN169ZpzJgx+vbbb7V3714FBQUpJCREHo9HL7/8sj799FNvqA0NDVV1dbV3dOfEE0/U6tWrVV9fr02bNh028PTq1UvJycmaPXu29u7dq+rqak2fPl033njjYYNIaz3zzDPauXOnKioq9Oc//1lj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iY477rg2LwoAAABoK83+loYbb7xREydOlMvlktvt1ty5c7V8+XLNmjXLl/UBAAAAR6TZI7ypqal6/vnnFRQUpDPPPFM//PCDnnzySe80BwAAACAQtWiEd/bs2ZoxY4YPywEAAADaVrNHeP/zn//I6Wx2PgYAAAACQrMT7K9//WtdffXVSk9P19FHH+39pob9PwMAAAACUbMD7zvvvCNJeu6555osdzgcBF50WGEhwQoP5S8XABCoIsL4jMaRcxhjjL+LAAAA+Clud4MqK6v9XUarORxSTEyUSkr2yPbU5etenc4gRUdHtny75q744+/gPdCQIUNa/MBAIKioqJLH0+jvMnzK4ZB69oxSaWnn+KClV/vQq51a0qvtzwV8r9mB99prr21yv7a2Vg6HQyeffLJyc3PbvDCgPRjTeT5I6dVO9GonegXaVrMDb0FBQZP7dXV1evLJJxUcHNzmRQEAAABtpdlfS/ZjoaGhmjx5spYuXdqW9QAAAABtqtWBV5I+//xzBQUd0S4AAAAAn2r2lAaXy9Xkfn19vbZu3arf//73bV4UAAAA0FaaHXivvPLKJveDgoJ00kknacCAAW1eFAAAANBWmh14d+zYoeuuu+6g5XPnztUdd9zRpkUBAAAAbeWwgXf37t3eb2d4+umndcopp+jA61Ts2bNHf//73wm8AAAACFiHDbxHHXWUnn76aZWXl6uurk5//OMfm/w8NDT0kKO+AAAAQKA4bOANDQ3V8uXLJUkTJ07UggUL2qUooL04HPtuNtvfn+19SvRqK3q108/1ysUo0JYcxrT+kPJ4PPrf//6n0047rS1rAgAAnZzb3aDKymp/l9EmHA4pJiZKJSWd45LRvuzV6QxSdHRky7dr7opvvvmmZs6cqV27djWZxxsWFnbQVdiAjmL6wve18btyf5cBADhARJhTi6ely+FgpBdto9mBd+7cucrKylJkZKQ2bNigcePG6S9/+YtGjRrly/oAn6p1N6imzuPvMgAAgA81+zJp27dv1/XXX6+0tDTt2LFDycnJmjdvnl566SVf1gcAAAAckWYH3piYGNXX1ysuLk7ffvutJKl3794qKSnxWXEAAADAkWp24E1MTNQdd9yh6upq9e3bVwsXLtTixYsVExPjy/oAAACAI9LswHvvvfeqR48eqq+v19SpU7V8+XItWrRId999ty/rAwAA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0Si8AAAAMJqXqwcAXMnXx1N+1fg2+K3qvnw+AABm4Scb3NrEwe1cPUKlZLUWyW539RQAAJQNCi/cWlZWrmy2YlePUa4sFikoKEAZGeecLrGUXQCASSi8cGt2u/uUO3fKCgDAb/GiNQAAABiNwgsAAACjUXgBAABgNAovAAAAjEbhBQAAgNEovAAAADAahRcAAABGo/ACAADAaLzxBNyaxXLhVhXwphEAANwYCi/cWmBgDVeP4DSrtUjZ2XmuHgMAgCqHwgu3Nn7eTv1wNNPVY1xXdV8vLRoXK4uFM70AAJQUhRdurcBapPzzNlePAQAAyhEvWgMAAIDRKLwAAAAwGoUXAAAARqPwAgAAwGgUXgAAABiNwgsAAACjUXgBAABgNAovAAAAjEbhBQAAgNEovAAAADAahRcAAABGo/ACAADAaBReAAAAGI3CCwAAAKNReAEAAGA0Ci8AAACMRuE1wJkzZ1RQUODqMQAAACqlCim8TZs21d13363Q0FDH7eGHHy6z7cfHxyslJUW7d+9WTExMmW23MruYWZLi4uKUlZUlSYqOjta+fftuaJvnz59XRESEhg8fftljhw8f1sCBAxUWFqbw8HANGDBAP/30k+Px6OhotWrVSqGhoWrVqpU6deqkadOmqbCw8IZmAQAAKCteFbWjDRs2qF69euWy7b/97W+SpN27d5fL9iuji5klOcpuaW3evFlt2rTRrl27lJGRoaCgIElSUVGRBg0apEGDBum9995TcXGx/vd//1cDBgzQF198IR8fH0nSggULFB4eLulCQR4+fLjy8vI0bty4MpkPAADgRrj8koajR4+qf//+ateunVq3bq0xY8aouLhYknTnnXdq8eLFatOmjTp16qTt27fr5ZdfVmhoqHr16qX09HRJVz6rGR0drZ07dzo+fu+99zRp0qRrzjJ69GjNmDFDCQkJCg0N1ZQpU7R27Vp17NhR7dq104YNGxzLfvrpp4qJiVHbtm01btw4nT9/vsTbuJL169fr8ccfd3zcp08fTZw4UdKF4hkZGan09HRH5r59+0qSunTpon/+85+SpC+++EKxsbEKCwvT1KlTr7m/30pKSlKXLl107733auXKlY77MzMzlZaWpq5du8rLy0s+Pj4aNGiQOnfurMzMzCtu6/e//70mTZqk5cuX68yZM9fc77Weq23btqlbt26KjIzU8OHDlZ2dLUlKTU3V448/rvDwcMXHxys5OdnpnAAAwL24vPCOHTtW7du319dff63k5GRt375dX3/9taQLBe/QoUP6+uuv9cgjj2jo0KGKiorSN998I19fXyUmJl51u7Gxsdq0aZPj440bN6pLly7XnWflypWaN2+ekpKStHjxYm3atEmbN2/W8OHDNW3aNEnS3r17NXPmTM2ZM0dffPGFsrOzNXv27BJt42ratWun77//Xvn5+bJarfrxxx8dZf67777TzTffrODgYMfyH330kaQLZ9CbNm0qSTp48KA+++wzrVy5UsuWLdPBgwevm/vXX3/VwYMHdd999+nhhx/Wp59+KrvdLkmqU6eOWrZsqd69e+v999/XgQMHZLPZNGnSJIWEhFx1m2FhYfL29r7u/q/2XB07dkwjR47UhAkT9NVXX6levXqaMGGCJGnmzJlq27at9u3bp1dffVWvv/66bDbbdXNWdRbLjd1Ks25Vu5HVzBtZzbyR1cxbeWa9URV2SUN8fLwsv5l08eLF+sMf/qCpU6eqbt26KigoUHp6umrVqqXTp087luvXr5+8vLwUERGhTz75RF27dpUktW7dWqdOnbrq/uLi4vTMM89o3Lhx+uWXX5Senu745/brzVm/fn1JUnBwsHr06KFq1aqpXbt2+utf/ypJWr16tR577DHdfvvtkqTnnntO/fr108iRI53extXUqlVLzZo1U0pKiry9vdWuXTt98803Onv2rHbu3KmOHTteN8PAgQPl7+8vf39/NW3aVL/88otatmx5zXXWrFmj2NhY+fn56Z577lFhYaF2796te+65R5K0aNEiLV68WBs3btSMGTMUGBiooUOHql+/ftfcbs2aNZWbm3vNZa72XL3//vuKiYlxPG/Dhg1TRESECgoKFBAQoG+++UZ333232rRpox07dlzy9WWqoKAAl6xb1ZDVTGQ1E1nNVNmyVljh/dvf/nbFa3h/+uknDRw4UHl5ebrzzjtVUFDgOLMoXShMkuTh4SF/f3/H/R4eHo5LH66kZcuWjrOLe/fu1QMPPCAPj+uf0A4I+L8nyNPTUzVq1JAkWSwWx/5OnTqltWvXatGiRY5lrVar47IGZ7ZxLR06dNDu3bvl7e2tiIgI5eXlKSUlRTt37rziC8qulcHb29upF46tWrVKp06d0pYtWyRJZ8+eVWJioqPw1qhR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cZo2bdo1X3BQGTmT9cCBA9q1a5fWrVunsLAwhYaGKjQ0VPPnz3ft8CXk7PNqAmezjh49WnfccYdiY2P15JNP6plnnqlyr/52NuusWbN04sQJtW/fXs8995xGjx6t0NBQF05etkw7Nl2LacemazHt2HQtlfXYZLFXtX/3AgAAAEqAM7wAAAAwGoUXAAAARqPwAgAAwGgUXgAAABiNwgsAAACjUXgBAJVKamqqq0cAYBgKLwBAffr00YIFC1w9hqZOnaqFCxe6eoxL7N69W3369FFYWJjCwsLUs2dPff75564eC0AJmPd+jACAKiszM1PVq1d39RgOx48f15AhQzR16lTdd999kqRt27bpxRdflL+/v9q1a+fiCQE4g8ILALjE7NmzlZqaqvz8fH311VcKDg7W5MmTtXLlSm3cuFGBgYGaNGmSOnTooN27d2vcuHG699579dlnn6lGjRoaNGiQ+vTpI0nKyMjQG2+8oe3bt8vDw0OdOnXSqFGjFBgYqJUrVyoxMVEWi0WHDx9W3759tXbtWlksFh09elQffvihPv/8c82bN0+pqamy2Wzq1KmTXnvtNfn5+Wn06NGqUaOG/vWvf+kf//iHbrnlFr3yyiuOErplyxbNnDlTqampuvnmm/Xyyy+rU6dOKioq0oIFC5SYmKhz586pdevWGj9+vEJCQi77XHz33Xfy9/fX/fffL09PT0nS/fffr+HDhys3N1eSZLfbNX/+fH388cc6e/asWrRooUmTJunWW28tUf558+apcePGev3117Vjxw5ZLBZ17dpVL774onx8fCro2QfMxCUNAIDLJCcnq1evXtq/f79atWqlJ598Um3atNHu3bsVFxenqVOnOpY9evSoCgoKtHPnTs2cOVPTp0/Xjh07JEnPPfeccnJytGHDBq1bt05ZWVkaOXKkY92UlBQNGDBAW7du1dNPP62EhAT16tVLH374oU6ePKmXXnpJo0aN0u7du7V69Wrt27dPycnJjvVXrlypF198Ubt371ZkZKQmTpwoSTp8+LCGDx+u5557Tvv27dOwYcP03HPPKTMzUx999JGSkpK0YMECbd++XbfddpueeeYZXemNRyMjI1VUVKRHH31UCxYsUEpKiqxWq/r376+YmBhJ0ooVK7R06VK999572rNnj5o1a6YRI0aUOH+LFi00atQo5ebmav369Vq9erV+/PFHzZgxowyfWcA9cYYXAHCZ5s2bq2PHjpIulL7du3froYcekiR16NBBn3zyiWNZHx8fjR49WtWqVVNYWJgSEhKUnJys2267Tfv379eXX36pWrVqSZLGjRunqKgo/frrr5KkmjVr6v7777/iDEFBQUpOTlbDhg2VnZ2t06dPq3bt2o51JalTp05q1aqVJKlbt25aunSpJGndunWKjIx0lNIHHnhAISEh8vPzU2Jiov785z/r1ltvlSSNGDFCERER+u6779SiRYtLZqhTp45WrVqlxYsXa9WqVXrzzTfl6+ur+Ph4vfLKK/L399fatWv1xBNPqFmzZpKk4cOH69///rdSU1NLlP/06dPaunWrtm/froCAAEnSCy+8oKeeekqjRo0q4TMI4LcovACAy9SuXdvx/56enqpZs6bjYw8Pj0vOhgYHB19y3W29evW0f/9+nT59Wl5eXqpXr57jsfr168vLy0snT56UJNWtW/eqM3h7e2vlypVasWKFqlWrpjvvvFMFBQWX7DsoKMjx/15eXo7H0tPTVb9+/Uu2d7EYnzhxQuPGjXOcDZak4uJipaWlXVZ4JSkkJEQjR47UyJEjde7cOe3atUtvvvmmJk6cqDfffFPp6emXZKxevbpatmyplJSUEuU/ceKEJCk+Pv6S/dtsNmVkZFySFUDJUHgBAJexWCxOL5uZmanCwkJ5e3tLulDc6tWrpwYNGshms+nkyZOO8pmWliabzaY6dero559/vuZ+kpOTtWrVKn366aeO0vjYY485NVO9evX07bffXnLfnDlzFBsbq5CQEI0ZM0ZRUVGOxw4fPqxbbrnlsu289NJL8vDwcFzCERAQoAceeEDnzp3Thx9+6NjXqVOnHOvk5ORo9uzZ6t+/f4nyh4SEyGKxaNu2bfL395ck5efn6z//+Y9uuukmp3IDuDKu4QUAlEpeXp5mzZolq9Wq/fv3629/+5u6d++ukJAQtW/fXq+++qqys7OVnZ2tV199VREREVcsl9KFyyPOnTsn6UJx9PDwkI+Pj2w2m1asWKG///3vKiwsvO5MXbt21d69e7VlyxYVFxdr8+bN+vDDDxUYGKgePXronXfeUVpamoqLi7V06VJ1795dWVlZV9zO+vXrtWLFCp05c0bFxcU6fPiwEhMTHZciPPjgg/rkk0/073//WzabTXPmzFFKSkqJ819c/rXXXlNOTo7y8vI0fvx4DRs2rES/gAC4HGd4AQCl4ufnp/z8fHXs2FE1a9bUxIkTFR4eLkmaNm2aXn/9dXXt2lVWq1X33nuvJk+efNVtxcXF6fnnn1fPnj21ZMkS7dmzR/fff7+qVaumVq1aqXv37vrpp5+uO9Ntt92m2bNna/r06Ro5cqRuvfVWzZ07V0FBQRowYIBsNpv69u2rzMxMNW7cWO+///4V/0pD586dNWvWLC1YsEBTp05VYWGh6tevr4cfflgDBw6UJD300EM6c+aMhgwZouzsbIWFhentt9++ofxvvvmmpk6dqi5duuj8+fMKCwvTnDlzrpsXwLVZ7Fd6WSoAAE7YvXu3hg4dqpSUFFePAgBXxSUNAAAAMBqFFwAAAEbjkgYAAAAYjTO8AAAAMBqFFwAAAEaj8AIAAMBoFF4AAAAYjcILAAAAo1F4AQAAYDQKLwAAAIz2/wDkFglB/p/LUQAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 640x1200 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "pos_features = feature_importances.loc[feature_importances.importance > 0]\n",
    "\n",
    "num = np.min([50, len(pos_features)])\n",
    "ylocs = np.arange(num)\n",
    "# get the feature importance for top num and sort in reverse order\n",
    "values_to_plot = pos_features.iloc[:num].values.ravel()[::-1]\n",
    "feature_labels = list(pos_features.iloc[:num].index)[::-1]\n",
    "\n",
    "plt.figure(num=None, figsize=(8, 15), dpi=80, facecolor='w', edgecolor='k');\n",
    "plt.barh(ylocs, values_to_plot, align = 'center')\n",
    "plt.ylabel('Features')\n",
    "plt.xlabel('Importance Score')\n",
    "plt.title('Positive Feature Importance Score - Logistic Regression')\n",
    "plt.yticks(ylocs, feature_labels)\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 941,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAArwAAAPRCAYAAAAfp3tzAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAMTQAADE0B0s6tTgAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAIABJREFUeJzs3XtclHX+///nwMhRNhGM0rLcLdjU1TxFhiWZLBpNRuKndm23tDLLNHerdXX7eKo0U7O0PJdmba12QIVVStZts8xMF9M+S9aaJooHREA5DgPX9w9/zi/yECDDDG8e99ttbjfnmrmueb5gGJ5eXNeMzbIsSwAAAICh/LwdAAAAAPAkCi8AAACMRuEFAACA0Si8AAAAMBqFFwAAAEaj8AIAAMBoFF4ATU5RUZGKioq8HaPevv/+e29HaHTNcWZT8b1EU0ThBVBnMTExevzxx89Y/tBDD2nevHkef/xf//rX2r9/vyRp4cKFGjNmTINuf968eerYsaO6detW45KUlHTB237zzTc1ffr0Bkj50+bNm6eHHnqoUR7rfP7xj3/o0Ucf9XaMGnJycjR27FjFxsaqW7duSkxM1IIFC1RdXe3taOf1+eefq1u3bg2+3dzcXHXr1k0FBQXnvd9//vMfDRkyxH39gQce0IoVK+r0WJ9//rliYmJq/Gxde+21SkxMVGpqar3ye0NSUpIyMzO9HQO1ZPd2AABNU3p6uvr27avbb7+90R+7sLDQ/e+RI0d65DFuvPFGLVq0qMG3W1BQoOb2eT9FRUU+NXN1dbUeeOABJSYm6tlnn1VISIh2796t0aNHy+l06rHHHvN2xEbXtm1bZWVl/eT9Tp48qcrKSvf1pUuX1uvxQkJCajyey+VSWlqaJkyYoK5du+rnP/95vbbbmP7+9797OwLqgD28AOrl7rvv1tSpU3Xw4MFz3uedd97RgAED1KtXL917773as2eP+7Z//OMfGjhwoHr27KnRo0fr0Ucfde8dPnz4sB599FHFx8erS5cuuuOOO/Tvf/9bktwF+5577lFqaqp7L2ZxcbG6du2qXbt2uR9j69atio2NldPpVFFRkcaPH68+ffroxhtv1PTp0+V0Ous1e1VVlRYvXqz+/fsrNjZWjzzyiI4cOeK+/W9/+5tuv/129ezZU7GxsZo8ebIsy9K6deu0aNEibdq0SYmJiZJO7S3/YeapU6fqz3/+s6RTe2hHjBghh8Oh66+/Xrm5uTp8+LBGjx6t66+/Xv369dPChQtrtVfy888/V1JSkl566SXFxsbq+uuv16pVq7R8+XL16dNH1113nZYsWeK+f0xMjJYuXao+ffqoZ8+emjhxoioqKtzzv/zyy7r55pvVq1cvDRs2TN98840k6cCBA+rWrZv+93//Vz179tSiRYs0adIk7dmzR926dVNVVZW++eYb3X///brxxhvVpUsX/eY3v9F3330nSXr//fc1bNgwTZgwQT179lR8fLxee+01d649e/Zo2LBh6t69u2666aYahWvjxo0aNGiQevbsqSFDhrifMz9WUFCgffv2yeFwKDQ0VDabTb/85S/1l7/8RUFBQTW2d/vtt6tbt2667bbb9PHHH9d5/uXLl//k86Uh5eTk6JFHHlFsbKz69u2r6dOnq7y8XJJUWVmpadOmKTY2VjfffLOWL1+ujh076sCBAzpw4IBiYmJ0/PhxVVdX65lnnlFcXJx69+6t4cOHa+/evTpy5IgefPBBlZaWqlu3bsrJydHvfvc7vfrqq5Kk4uJiTZgwQdddd51iY2M1fvx492P/FLvdruTkZP3sZz9zfy0rKio0Y8YMxcfH64YbbtCf//xnnThxwr3OwoUL1adPH/Xp00ezZ89Wv3799Pnnn0s69fx9+umndd1112natGmSzv16dK55JWnv3r2655571LNnT91yyy2aPn26qqqqJEn9+vVTRkaGJCk/P1/jxo1T7969FRcXp/Hjx7v/Y/5Tz2k0DgovgHpJSUnR9ddfrz/96U9nLVwffvihXnzxRc2ePVubN2/WLbfcovvvv19lZWX6/vvvNXbsWI0dO1ZbtmxRfHy8NmzY4F73qaeeUlRUlD788EN98cUX6tixo2bNmiVJWrt2raRThwYkJye712nZsqX69++vtLQ097K1a9fqtttuU0BAgMaNG6eSkhKtX79ea9as0ddff605c+bUa/YVK1YoNTVVr776qj7++GNdeeWVGjVqlCzL0pdffqkXXnhBs2fP1rZt2/T6668rNTVVW7Zs0a233qqHHnpIN954oz744INaPdbmzZv17LPPasOGDYqKitLIkSMVFRWljz76SCtWrNDf//53vfXWW7Xa1n//+1/ZbDZt3rxZf/jDHzR58mR999132rhxo2bMmKEXXnhBx48fd9//ww8/VGpqqv7+978rKytLL7/8sqRTRTwtLU2vvvqqPv30U/Xq1UvDhw93l5HS0lK1bNlSmzdv1tChQzVlyhT94he/UFZWlvz9/fXYY48pNjZW//rXv7R582aFhoZqwYIFNWbu3LmztmzZoieffFIzZ87U4cOHVVlZqQcffFAdO3bUZ599pmXLlunVV1/VRx99pF27dunxxx/Xn//8Z23ZskX333+/HnroIR09evSMr0NERIR69eqlBx98UHPmzNGmTZt04sQJxcfHuw8B2bNnjx577DGNHj1a27Zt05gxYzR69GgVFBTUaf6UlJTzPl8aktPp1LBhw3TxxRfro48+0qpVq7Rjxw534Vu0aJE2b96s1NRUrVmzRp999pm7vP3Qhg0b9PnnnysjI0Mff/yxoqKiNHfuXEVFRWnJkiXuvbOXX355jfUmTZqk3NxcZWRkaMOGDdq/f79eeumlWmWvqKjQsmXL5HQ6de2110qSZs6cqS+//FLvvPOOPvzwQ1VWVuqpp56SJK1evVpvvvmmXnvtNWVmZqqgoOCM/3wfP35cmzZt0ujRo8/7enSueSVpxowZio2N1RdffKE33nhD69ev1yeffHJG/tGjR6u4uFgZGRlat26dCgsL9cQTT7hvP9dzGo3IAoA6io6Otnbu3GkdP37c6tOnjzV//nzLsixrxIgR1ty5cy3Lsqz777/fWrBgQY31EhMTrfXr11uvvPKKNXz48Bq3DRkyxL3uoUOHrNLSUquiosLas2ePNX36dKtfv35nPL5lWdbcuXOtESNGWJZlWZ988okVFxdnVVVVWRUVFVbPnj2tXbt2WXl5eVZ0dLR1+PBh9zaysrKsa6+99qzzzZ071+rYsaPVo0ePGpevv/7asizLGjBggLV27Vr3/SsrK61rr73W2rlzp1VWVmbl5uZalmVZ+fn51tatW624uDgrNTX1jLw/nsWyLGvKlCnWuHHj3PcdNGiQ+7YdO3ZYXbt2tZxOp3tZenq6lZSUdM45Tj/Wli1brJiYGKu0tNSyLMv6/vvvrejoaGvfvn2WZVlWVVWVFR0dbX311VfuXJs3b3ZvKy0tzYqPj7csy7L69u1rrV69usZj9e/f31q7dq2Vk5NjRUdHW9nZ2e7b3nvvvRoZ9+/fb1VWVlplZWXW7t27rccff9z63e9+577v9ddfX2PbnTt3trZu3Wpt2bLF6tatW435v/32Wys/P9+aOHGi9dRTT9VYb/jw4dbSpUvP+rUpLy+3li1bZv32t7+1OnfubP3yl7+0hg0bZu3Zs8f9tfvxc3THjh1WWVlZnec/3/OlrrZs2XLO5+3mzZutrl27WhUVFe5lX3zxhfWrX/3Kqqqqsvr372+lpaW5b/vvf/9rRUdHWzk5Oe7c+fn51ubNm63u3btby5Yts/bu3WtVVVWd8/Hvuecea+nSpVZFRYXVqVMnKysry33boUOH3M+vH88QHR1t9ejRw+revbvVuXNnq0uXLtajjz5q7dq1y7Isy6qurra6dOlibd++3b3e0aNH3Rnvvfdea+HChe7biouLrWuuucbasmWLZVmnnr8bNmxw336+16Pzzfvkk09ad911l/XBBx9YJ06cqHHbzTffbK1fv97av3+/FR0dbR06dMh9W25urvs153zPaTQejuEFUG/h4eGaMWOGRowYobi4uBq35ebmauHChTX+5Oxyudx/lr/00ktr3L9du3buf+/du1czZ85Ubm6urrrqKoWGhtZqb1jv3r1lt9u1ZcsWnThxQpdccok6d+6snTt3StIZJ525XC7l5+crIiLijG316dPnnMfw5ubmauLEiZoyZYp7WXV1tQ4ePKiYmBgtWrRIGRkZatWqlTp16qTq6up6nwx18cUXu/998OBBVVRUqHfv3u5llmXJz692f6wLCgpScHCwJLnXCQsLq3H9hznbt2/v/vcll1yivLw8SdKxY8dqfL+kU9+/Q4cOuU+o+mHuH9u1a5ceeughnThxQldffbVcLleN23/8/bDb7aqurtaxY8cUGRmpFi1auG+76qqrJJ36nnz++edav369+7aqqip16NDhrBkCAwN133336b777pPT6dTOnTs1f/58PfDAA9qwYYPy8vLOeI527dq1XvOf7/nyq1/9qsZ2fnhCmsPh0NSpU8+a/2zy8/PVpk0bBQQEuJdddtllqqioUH5+/hk/d5dddtlZt9O7d29NnjxZb7/9tmbNmqV27drpT3/6k2655ZZzPnZRUZEqKytrbP+SSy455/1DQkK0bds2SdLXX3+t0aNHKyoqSp07d5Z0au9seXm5HnzwQdlsNvd6gYGBOnDgwBmzhIaGKjw8vMZj/Ph7cK7XowEDBpxz3okTJ2revHl6/vnndejQId14442aMmWKoqKi3Ns5duyY7HZ7jXkvvfRS2e12HTp0SNK5n9NoPBReABfkhhtu0NChQ/Xkk0/W+AUTFRWloUOHaujQoe5l+/btU5s2bbRixQr3L7vTDh06pJ///OdyOp165JFHNHnyZA0aNEiStHLlSn377bc/mcXPz0+DBg1y/0nx9CEPUVFRstls+uijj9SyZUtJUllZmY4eParWrVvXeeaoqChNmDBB8fHx7mV79uzRZZddptdee027du3SBx98oIsuukjSqfJ8vsw/PAmosLCwRmH54S/7qKgotWrVSp999pl7WVFRkU6ePFmr3D/cVm0cOXLEXexyc3PdBaNt27Y6cOCAevbsKelU6c7JyVFkZORPbvPw4cN64okn9Prrr6tXr16SpBdeeKFWJ0xFRUUpLy9PLpdLdvupX1/p6ekKDQ11P9/GjRvnvn9OTo77e/BDK1eu1JIlS7RhwwbZbDYFBASoZ8+emjJlivr376+ioiJdcsklZxwDPH/+fCUmJtZ5/vM9X36sNl+Hc7n00kuVl5cnp9Ppfg7t379fLVq00EUXXaRLL720xp/RT5exH8vJyVF0dLTeeustFRcX66233tLYsWO1ffv2cz52RESEWrRoocOHD7vL4M6dO/Xvf/9b991333lz//KXv9T8+fOVkpKiqKgoPfjggwoPD1dAQID+9re/6eqrr5Z0qqB+//33uuKKK86Ypby8vMbJrNKZPzvnej0637zZ2dkaNWqUxo8fr++//15PPfWU5syZo+eee869nbZt28rlcunQoUPun5GDBw/K5XIpMjLSfXw6vItjeAFcsMcff1yBgYHaunWre9ngwYO1bNkyffPNN7IsS5mZmbrtttu0d+9e3X777dq2bZv++c9/qqqqSunp6e5f9JWVlXI6ne6Th3bv3q3XXnutxglmAQEBKi4uPmuW5ORkbdy4UZs3b3af4BYVFaW4uDhNmzZNxcXFKi0t1aRJkzRmzJg6l8DTs7388ss6ePCgqqur9de//lXJyckqLCxUcXGxWrRoIbvdrvLycr3yyivKy8tzl9rAwMAa2a+88kqlpaWpurpaO3bscJ8YdTZdunRRRESEXnrpJVVUVKiwsFBjx47Vs88+W+cZamPevHkqKirSoUOHtGTJEvd/IO68804tWLBA3333nZxOpxYsWKDi4uIahe6HAgMD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AABgNLu3AwA/ZeDAgQoNDdW7777rXrZ48WLNnTtXLVq0kCSFhITo008/9VZEAADgwyi88Gk7duxQq1atdPToUWVnZ+uaa66RJO3evVuTJ09WSkqKlxMCAABfxyEN8GmpqamKj4+Xw+HQypUr3ct3796t6OhoLyYDAABNBYUXPsvpdCojI0MOh0PJyclKT09XWVmZnE6n9u7dq/nz56t3794aMmSIsrKyvB0XAOBBNlvTvpgwgy/MWl8c0gCflZmZqU6dOqlt27aSpJiYGK1bt05xcXHq3r277rvvPnXv3l1paWkaOXKkPvzwQ1100UVeTg0A8ISIiDBvR7hgJsxQW742K4UXPis1NVVZWVmKi4uTJJWUlMjlcmnw4MF644033PcbPHiwli9frh07dqhv377eigsA8KD8/JOyLG+nqB+b7VQBbMoz1JanZ/X391N4eGid16Pwwifl5eVp69atSktLU3BwsCSpvLxcSUlJ2r17tz799FMNHz7cfX+n06mAgABvxQUAeJhlqcmXRRNmqC1fm5XCC5+0Zs0axcbGqn379jWWx8fHa/ny5crIyNDVV1+tG264QW+//bYqKyvVo0cPL6UFAAC+jJPW4JNWr16txMTEM5Y7HA5lZmZq5syZmjZtmnr06KG0tDQtWLCAPbwAAOCs2MMLn5Senn7W5QkJCUpISJAk9e/fvzEjAQCAJqree3gPHjyowsLChswCAAAANLhaF96dO3fq7rvvliS98847uuWWW3TTTTdp48aNHgsHAAAAXKhaH9IwY8YMxcXFybIszZ8/X88//7xatWqlGTNmqF+/fp7MCAAAANRbrffw7tmzR6NHj9Y333yjgoICDRgwQDfddJNyc3M9mQ8AAAC4ILUuvEFBQcrPz1dmZqZ69OihgIAA7d69W+Hh4Z7MBwAAAFyQWh/ScPfdd2vQoEEqLi7WK6+8ol27dumBBx7Qww8/7Ml8AAAAwAWpdeEdOXKkbrzxRrVs2VJXXHGFjh49qjlz5uiGG27wZD4AAADggtTpbcmioqK0ceNGPfvsswoJCVFpaamncgEAAAANotaFNysrS0lJSfr000/13nvvqbCwUOPGjdNbb73lyXwAAADABal14X3uuef09NNPa+nSpfL399dll12mxYsXa/ny5R6MBwAAAFyYWhfe7777zv1RrjabTZLUo0cPHT9+3DPJ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AAAwGoUXAAAARqPwAgAAwGgUXgAAABiNwgsAAACjUXgBAABgNAovAAAAjEbhdVNxcXF65JFHynUfs2fPVtOmTZWYmHjZYw888IBiYmLKdf8AAAAShdctHThwQIGBgcrMzNQPP/xQrvsKDAzUxo0bL7nv+++/V3p6ernuFwAA4CIKrxtKSkpSVFSUEhIStHz5csf927dvV2xsrNq0aaMpU6YoOjpav/zyiyTp73//u3r06KHw8HD1799fJ0+edGpf7du314EDB5Sdne24b/369YqOjr5kublz56pTp05q27atxowZo5ycHElSnz59NGvWLD3wwAOOuex2uyRp3rx56tChg9q3b6/nnntOZ8+eLdXnBQAAmInC62asVqs2bNighIQEde/eXcnJycrPz9eZM2f0wgsv6JVXXtGOHTtUVFSktLQ0SdLZs2c1ePBgDR48WLt27VKnTp30/PPPO7U/Pz8/tW3bVlu2bHHct3nz5ksuZ0hKStKaNWv08ccfa9OmTcrKytJrr712yfKffPKJEhMT9dlnn+nbb7/V0aNHtXDhQq1evVpbt26VzWbT6tWry+izhKuxWCr/rarMSVaykpWspt7KM+uN8rrxVVEVbd68Wc2bN1eDBg0kSU2bNtW6devk4eGhu+66S1FRUZKkF198UZ988okkadu2bbrjjjsUGxsrSXryySc1b948/fzzz/rd73533X126dJFycnJ6t69u/7xj3/o5ptvVu3atR2PJycna+DAgbrlllskSS+99JIefPBBTZ48WZL08MMPKygoSEFBQfrDH/6g1NRU3XLLLcrLy1NSUpK6dOmiOXPmyFKa7wQ4JSgowNUjOKWqzFkWyGomspqJrK5D4XUzSUlJSklJUfv27SVJubm5stlsio6OVkhIiGM5Pz8/Ryk9deqUUlJSFB4e7ni8sLBQJ0+edKrwdu7cWRMmTFBOTo7Wr1+vuLi4Sx4/ceKEo4BLUoMGDXT+/HllZmZK0iXl2NPTU8XFxQoJCdGsWbM0b948zZgxQ7fffrsmT56s5s2b38BnBc7KyDin/39FSaVksVw4yFb2OcsCWc1EVjORtex4enqodu0aJV6PwutG0tPTtWfPHq1du1Z+fn6SpIKCAsXHx6tjx46XXJd7/vx5ZWVlSZKCg4PVsWNHzZ071/H44cOH1bBhQ6f2W6NGDUVGRmrr1q364osvNGTIEP3444+Ox+vWrasTJ044Pk5LS5O3t7cCAq7+2+GZM2d00003aenSpcrOzta7776rCRMmaMWKFc59MnBD7HZViYN1VZmzLJDVTGQ1E1ldh2t43cjq1avVpk0bNWrUSMHBwQoODlbDhg0VFRXl+IsNX375pQoLCzVr1iwVFhZKku69916lpKTo66+/lt1u14YNG/TII48oLy/P6X136dJF7777rm699VbVqlXrkse6deumDz74QL/88otycnI0bdo0PfDAA/L29r7q9tLS0jRo0CAdOXJENWvWlL+//2XbBQAAkCi8bmXVqlWO63B/KyEhQWvWrNG0adM0adIkdejQQXa7Xd7e3vL29tZNN92k2bNn66233lLr1q01Z84czZkzR4GBgU7vOzo6WmlpaZddziBJPXr0ULdu3fTEE08oKipK/v7+mjhx4jW316JFCw0ePFhPPvmkwsLCtHfvXo0fP97peQAAgPuw2O2V6YQzXCUjI0Pp6elq1qyZpAuXOoSGhurbb791XP5golHv7NChI2dcPUal51fNS4mvxev06cp9/ZnFItWpE1Dp5ywLZDUTWc1E1rLj5XVj1/ByhheSpLy8PPXt21fHjh1TUVGRPvjgA4WGhhpddgEAgHvgRWuQJDVs2FAjR45Uv379lJ2drZYtW2rq1KnXXGfr1q0aMWLEFR9r2rSpli1bVh6jAgAAlAiFFw69evVSr169nF6+c+fOSklJKceJAAAASo9LGgAAAGA0Ci8AAACMRuEFAACA0Si8AAAAMBqFFwAAAEaj8AIAAMBoFF4AAAAYjcILAAAAo1F4AQAAYDQKLwAAAIxG4QUAAIDRKLwAAAAwGoUXAAAARqPwAgAAwGherh4AcCVfH0/5VePb4Hqq+/I5AgBUXfwUg1ubOLidq0eoMqzWItntrp4CAICSo/DCrWVl5cpmK3b1GOXKYpGCggKUkXGuVIWVsgsAqKoovHBrdrv7FDl3ygoAwG/xojUAAAAYjcILAAAAo1F4AQAAYDQKLwAAAIxG4QUAAIDRKLwAAAAwGoUXAAAARqPwAgAAwGi88QTcmsVy4Wayi/lKkpM3qAAAmITCC7cWGFjD1SNUmKCgAKeXtVqLlJ2dV47TAABQcSi8cGvj5+3UD0czXT1GpVLd10uLxsXKYuFMLwDADBReuLUCa5Hyz9tcPQYAAChHvGgNAAAARqPwAgAAwGgUXgAAABiNwgsAAACjUXgBAABgNAovAAAAjEbhBQAAgNEovAAAADAahRcAAABGo/ACAADAaBReAAAAGI3CCwAAAKNReAEAAGA0Ci8AAACMRuEFAACA0Si8AAAAMBqFFwAAAEaj8FZRTZs21alTp8p9PzExMdq9e7dOnDih8PDwct8fAABAWaPwwikNGjTQvn37XD0GAABAiVF4q7iVK1eqW7duCg0NVXR0tDZs2OC4v1+/fo7lVq9erT59+kiSRo8erSlTpuiPf/yjIiIiNGrUKJ0/f16SdPjwYfXs2VOhoaEaM2aMioqKJEm//PKL7rzzTsf2Fi1apE6dOikyMlKvvPKKCgsLJUnbtm1Tt27dFBkZqeHDhys7O/ua86empqply5bKzc113Ne/f39t2LBBdrtd77//vjp37qwOHTpo5syZKi4uliR9+eWX6tKliyIjI9W7d2/98MMPpfxMAgAAU1F4q7Djx49r6tSpmj17tr799ls9/fTTevXVV51ad926dXr33Xe1ceNG7du3Txs3bpQkPf/88+rcubP27NmjO+64Q2lpaZetu2XLFi1cuFALFy7U1q1bdfz4cS1evFjHjh3TyJEjNWHCBH311VeqV6+eJkyYcM05GjZsqCZNmmj79u2SpKysLB08eFD33nuvVq1apTVr1ujjjz/W2rVrtXfvXi1fvlySNHbsWE2YMEF79uxR586dNXfu3BJ85uAMi6Vq3qry7GQlK1nNvZG17LZ9I7xufFW42s0336xVq1apfv36Sk9Pl4+Pj9LT051at0uXLmrYsKEkKSIiQqmpqTp+/LiOHz+uQYMGydvbW08++aQ++OCDy9bdsGGDevbsqd///veSpGnTpslut2v16tWKiYlxXOs7bNgwRUREqKCgQL6+vledJS4uTps3b3b8t3379vLz89OaNWs0cOBA1a9fX5I0ePBgzZkzR71791ZAQICSk5Pl7++vgQMHysOD393KWlBQgKtHuGFVefaSIquZyGomsroOhbeKW7hwodasWaPg4GDdcccdTq9Xu3Ztx/97enqquLhY6enpql27try9vSVJFotFISEhl62bkZGhyMhIx8cXC+mpU6eUnJysTZs2OR7z8vLSyZMn1bhx46vOEhcXp/fff19Wq1Wff/65Hn74Ycf2Jk2apMmTJ0uS7Ha7atWq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67natm2bunXrpsjISA0fPlzZ2dmSpNTUVD3++OMKDw9XfHy8kpOTnc4JAADci8sL79ixY9W+fXt9/fXXSk5O1vbt2/X1119LulDwDh06pK+//lqPPPKIhg4dqqioKH3zzTfy9fVVYmLiVbcbGxurTZs2OT7euHGjunTpct15Vq5cqXnz5ikpKUmLFy/Wpk2btHnzZg0fPlzTpk2TJO3du1czZ87UnDlz9MUXXyg7O1uzZ88u0Taupl27dvr++++Vn58vq9WqH3/80VHmv/vuO918880KDg52LP/RRx9JunAGvWnTppKkgwcP6rPPPtPKlSu1bNkyHTx48Lq5f/31Vx08eFD33XefHn74YX366aey2+2SpDp16qhly5bq3bu33n//fR04cEA2m02TJk1SSEjIVbcZFhYmb2/v6+7/as/VsWPHNHLkSE2YMEFfffWV6tWrpwkTJkiSZs6cqbZt22rfvn169dVX9frrr8tms103Z1VnsdzYrTTrVrUbWc28kdXMG1nNvJVn1htVYZc0xMfHy/KbSRcvXqw//OEPmjp1qurWrauCggKlp6erVq1aOn36tGO5fv36ycvLSxEREfrkk0/UtWtXSVLr1q116tSpq+4vLi5OzzzzjMaNG6dffvlF6enpjn9uv96c9evXlyQFBwerR48eqlatmtq1a6e//vWvkqTVq1frscce0+233y5Jeu6559SvXz+NHDnS6W1cTa1atdSsWTOlpKTI29tb7dq10zfffKOzZ89q586d6tix43UzDBw4UP7+/vL391fTpk31yy+/qGXLltdcZ82aNYqNjZWfn5/uueceFRYWavfu3brnnnskSYsWLdLixYu1ceNGzZgxQ4GBgRo6dKj69et3ze3WrFlTubm511zmas/V+++/r5iYGMfzNmzYMEVERKigoEABAQH65ptvdPfdd6tNmzbasWPHJV9fpgoKCnDJulUNWc1EVjOR1UyVLWuFFd6//e1vV7yG96efftLAgQOVl5enO++8UwUFBY4zi9KFwiRJHh4e8vf3d9zv4eHhuPThSlq2bOk4u7h371498MAD8vC4/gntgID/e4I8PT1Vo0YNSZLFYnHs79SpU1q7dq0WLVrkWNZqtToua3BmG9fSoUMH7d69W97e3oqIiFBeXp5SUlK0c+fOK76g7FoZvL29nXrh2KpVq3Tq1Clt2bJF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gNEovAAAADAahRcAAABGo/ACAADAaBReAAAAGI3CCwAAAKNReAEAAGA0Ci8AAACMRuEFAACA0Si8AAAAMBqFFwAAAEaj8AIAAMBoFF4AAAAYjcILAAAAo1F4AQAAYDQKLwAAAIxG4QUAAIDRKLwAAAAwGoUXAAAARqPwAgAAwGgUXgAAABiNwgsAAACjUXgBAABgNAovAAAAjEbhBQAAgNEovAAAADAahRcAAABGo/ACAADAaBReAAAAGI3CCwAAAKNReAEAAGA0L1cPALiSp6f7/M5HVjOR1UxkNRNZXbddi91ut5fxLAAAAECl4T6/agAAAMAtUXgBAABgNAovAAAAjEbhBQAAgNEovAAAADAahRcAAABGo/ACAADAaBReAAAAGI3CCwAAAKNReAEAAGA0Ci+Mtn//fiUkJOjuu+/WU089pdOnT1+2TF5enoYPH66wsDBFR0friy++cMGkpedM1tTUVA0YMEDh4eGKjo7W8uXLXTBp6TmT9SKr1ar4+HitXLmyAicsO85kLSoq0vTp0xUVFaW2bdtq7ty5Lpi09JzJmp2drWeffVYRERHq3LmzVqxY4YJJy86CBQv0l7/85YqPmXJsuuhaWU05Nl10rawXVfVj00XXylqZjk0UXhiroKBAw4YN07Bhw7Rnzx7deuutev311y9bbvr06fLw8NCuXbs0efJkvfLKKzp37pwLJr5xzmZ9+eWX1bJlS33zzTeaM2eOpk+frpSUFBdMfOOczXrRu+++q59//rkCJyw7zmadP3++9u7dq1WrVumzzz7TsmXL9M0337hg4hvnbNZ33nlHtWrV0s6dO/Xee+9p8uTJSk1NdcHEpVNYWKhZs2Zp2rRpV13GhGOT5FxWE45NknNZL6rKxybJuayV6dhE4YWxdu3apZCQEMXExMjHx0fPP/+8Nm7cqLy8vEuWS05O1tChQ1WtWjW1bdtWrVu31vr161009Y1xJqvVapW/v78GDRokLy8vNWvWTG3atNHBgwddOHnJOfu8StKhQ4f01VdfKTw83AWTlp6zWT/99FONHj1agYGBatCggZYsWaKmTZu6aOob42zW48ePy263y263y2KxyNvbW56eni6a+sa9+uqr+u677/Too49edRkTjk3S9bOacmySnHtepap/bJKcy1qZjk0UXhjr2LFjuu222xwfBwYGqnr16jp+/LjjvuzsbGVmZqpx48aO+2677TYdPny4IkctNWey+vj4aP78+apevbokKScnR/v3769yxciZrNKFsw9jx47VpEmTqmQhkpzLmpubq9TUVP3rX/9STEyMOnfurG3btql27doumPjGOfu8Pv7441q/fr3uvvtuJSQk6Nlnn1WDBg0qeNrSe/bZZzVv3jwFBQVd8XFTjk3S9bOacmySrp9VMuPYJF0/a2U7Nnm5ZK9ABcjLy1O1atUuuc/Pz08FBQWOj/Pz82WxWOTj4+O4z9fXVxkZGRU2Z1lwJutvnT9/XsOHD9fdd9+te+65pyJGLDPOZn3//ffVtm1bNW/evCLHK1POZL34T9xbt25VUlKSTp06pX79+qlJkyZq27Zthc5bGs4+r4WFherfv78GDRqkQ4cO6emnn1ZYWJhatGhRkeOWWnBw8DUfN+XYJF0/629V5WOT5FxWE45N0vWzVrZjE2d4YSw/Pz9ZrdZL7svPz3ecRZAu/ACx2+2XLFdQUKAaNWpU2JxlwZmsF2VnZ+upp56SxWLR9OnTK2rEMuNM1p9++kkbNmzQsGHDKnq8MuVM1ouFaMiQIfL391eTJk3UrVs3ffnllxU6a2k5k9VqtWrUqFHq06ePfH19FRYWpvj4eCUnJ1f0uOXOlGNTSVT1Y5MzTDk2OaOyHZsovDBW48aNdfToUcfHWVlZys3NVaNGjRz3BQYGqnbt2jp27JjjviNHjuh3v/tdRY5aas5klaTTp0+rd+/euvnmmzV37tzLzqhVBc5k/eKLL5SWlqb27dsrPDxce/fu1cSJEzVv3jwXTHzjnMlau3Zt1axZUzk5OY77bDab7HZ7RY5aas5kzcvLU05OjoqLix33eXp6ysvLvH+sNOXY5CwTjk3OMOXY5IzKdmyi8MJY99xzj06ePKn169fLarVq5syZio6Olq+v7yXLde3aVbNnz1Z+fr527dql/fv3Kzo62kVT3xhns44cOVKtWrXSG2+8IW9vbxdNWzrOZH366aeVkpKiffv2ad++fYqIiND48eM1ePBgF05ecs5ktVgs6tatm959913l5OTo8OHDSk5OVkxMjAsnLzlnsgYGBurOO+/UjBkzZLVa9eOPP2rt2rW6//77XTh5+THh2OQsE45NzjDl2OSMynZsovDCWL6+vpo7d67ee+89tWnTRqmpqZowYYIkKTQ0VPv27ZMkjRgxQj4+PurUqZPGjRunadOmXfMFB5WRM1kPHDigXbt2ad26dQoLC1NoaKhCQ0M1f/581w5fQs4+ryZwNuvo0aN1xx13KDY2Vk8++aSeeeaZKvfqb2ezzpo1SydOnFD79u313HPPafTo0QoNDXXh5GXLtGPTtZh2bLoW045N11JZj00We1X7dy8AAACgBDjDCwAAAKNReAEAAGA0Ci8AAACMRuEFAACA0Si8AAAAMBqFFwBQqaSmprp6BACGofACANSnTx8tWLDA1WNo6tSpWrhwoavHuMTu3bvVp08fhYWFKSwsTD179tTnn3/u6rEAlIB578cIAKiyMjMzVb16dVeP4XD8+HENGTJEU6dO1X333SdJ2rZtm1588UX5+/urXbt2Lp4QgDMovACAS8yePVupqanKz8/XV199peDgYE2ePFkrV67Uxo0bFRgYqEmTJqlDhw7avXu3xo0bp3vvvVefffaZatSooUGDBqlPnz6SpIyMDL3xxhvavn27PDw81KlTJ40aNUqBgYFauXKlEhMTZbFYdPjwYfXt21dr166VxWLR0aNH9eGHH+rzzz/XvHnzlJqaKpvNpk6dOum1116Tn5+fRo8erRo1auhf//qX/vGPf+iWW27RK6+84iihW7Zs0cyZM5Wamqqbb75ZL7/8sjp16qSioiItWLBAiYmJOnfunFq3bq3x48crJCTkss/Fd999J39/f91///3y9PSUJN1///0aPny4cnNzJUl2u13z58/Xxx9/rLNnz6pFixaaNGmSbr311hLlnzdvnho3bqzXX39dO3bskMViUdeuXfXiiy/Kx8engp59wExc0gAAuExycrJ69eql/fv3q1WrVnryySfVpk0b7d69W3FxcZo6dapj2aNHj6qgoEA7d+7UzJkzNX36dO3YsUOS9NxzzyknJ0cbNmzQunXrlJWVpZEjRzrWTUlJ0YABA7R161Y9/fTTSkhIUK9evfThhx/q5MmTeumllzRq1Cjt3r1bq1ev1r59+5ScnOxYf+XKlXrxxRe1e/duRUZGauLEiZKkw4cPa/jw4Xruuee0b98+DRs2TM8995wyMzP10UcfKSkpSQsWLND27dt122236ZlnntGV3ng0MjJSRUVFevTRR7VgwQKlpKTIarWqf//+iomJkSStWLFCS5cu1Xvvvac9e/aoWbNmGjFiRInzt2jRQqNGjVJubq7Wr1+v1atX68cff9SMGTPK8JkF3BNneAEAl2nevLk6duwo6ULp2717tx566CFJUocOHfTJJ584lvXx8dHo0aNVrVo1hYWFKSEhQcnJybrtttu0f/9+ffnll6pVq5Ykady4cYqKitKvv/4qSapZs6buv//+K84QFBSk5ORkNWzYUNnZ2Tp9+rRq167tWFeSOnXqpFatWkmSunXrpqVLl0qS1q1bp8jISEcpfeCBBxQSEiI/Pz8lJibqz3/+s2699VZJ0ogRIxQREaHvvvtOLVq0uGSGOnXqaNWqVVq8eLFWrVqlN998U76+voqPj9crr7wif39/rV27Vk888YSaNWsmSRo+fLj+/e9/KzU1tUT5T58+ra1bt2r79u0KCAiQJL3wwgt66qmnNGrUqBI+gwB+i8ILALhM7dq1Hf/v6empmjVrOj728PC45GxocHDwJdfd1qtXT/v379fp06fl5eWlevXqOR6rX7++vLy8dPLkSUlS3bp1rzqDt7e3Vq5cqRUrVqhatWq68847VVBQcMm+g4KCHP/v5eXleCw9PV3169e/ZHsXi/GJEyc0btw4x9lgSSouLlZaWtplhVeSQkJCNHLkSI0cOVLnzp3Trl279Oabb2rixIl68803lZ6efknG6tWrq2XLlkpJSSlR/hMnTkiS4uPjL9m/zWZTRkbGJVkBlAyFFwBwGYvF4vSymZmZKiwslLe3t6QLxa1evXpq0KCBbDabTp486SifaWlpstlsqlOnjn7++edr7ic5OVmrVq3Sp59+6iiNjz32mFMz1atXT99+++0l982ZM0exsbEKCQnRmDFjFBUV5Xjs8OHDuuWWWy7bzksvvSQPDw/HJRwBAQF64IEHdO7cOX344YeOfZ06dcqxTk5OjmbPnq3+/fuXKH9ISIgsFou2bdsmf39/SVJ+fr7+85//6KabbnIqN4Ar4xpeAECp5OXladasWbJardq/f7/+9re/qXv37goJCVH79u316quvKjs7W9nZ2Xr11VcVERFxxXIpXbg84ty5c5IuFEcPDw/5+PjIZrNpxYoV+vvf/67CwsLrztS1a1ft3btXW7ZsUXFxsTZv3qwPP/xQgYGB6tGjh9555x2lpaWpuLhYS5cuVffu3ZWVlXXF7axfv14rVqzQmTNnVFxcrMOHDysxMdFxKcKDDz6oTz75RP/+979ls9k0Z84cpaSklDj/xeVfe+015eTkKC8vT+PHj9ewYcNK9AsIgMtxhhcAUCp+fn7Kz89Xx44dVbNmTU2cOFHh4eGSpGnTpun1119X165dZbVade+992ry5MlX3VZcXJyef/559ezZU0uWLNGePXt0//33q1q1amrVqpW6d++un3766boz3XbbbZo9e7amT5+ukSNH6tZbb9XcuXMVFBSkAQMGyGazqW/fvsrMzFTjxo31/vvvX/GvNHTu3FmzZs3SggULNHXqVBUWFqp+/fp6+OGHNXDgQEnSQw89pDNnzmjIkCHKzs5WWFiY3n777RvK/+abb2rq1Knq0qWLzp8/r7CwMM2ZM+e6eQFcm8V+pZelAgDghN27d2vo0KFKSUlx9SgAcFVc0gAAAACjUXgBAABgNC5pAAAAgNE4wwsAAACjUXgBAABgNAovAAAAjEbhBQAAgNEovAAAADAahRcAAABGo/ACAADAaP8P/0cgX3OZr/0AAAAASUVORK5CYII=\n",
      "text/plain": [
       "<Figure size 640x1200 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "neg_features = feature_importances.loc[feature_importances.importance < 0]\n",
    "\n",
    "num1 = np.min([50, len(neg_features)])\n",
    "\n",
    "values_to_plot1 = neg_features.iloc[-num1:].values.ravel()\n",
    "feature_labels1 = list(neg_features.iloc[-num1:].index)\n",
    "\n",
    "plt.figure(num=None, figsize=(8, 15), dpi=80, facecolor='w', edgecolor='k');\n",
    "plt.barh(ylocs, values_to_plot, align = 'center')\n",
    "plt.ylabel('Features')\n",
    "plt.xlabel('Importance Score')\n",
    "plt.title('Negative Feature Importance Score - Logistic Regression')\n",
    "plt.yticks(ylocs, feature_labels)\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 942,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "RandomForestClassifier(bootstrap=True, class_weight=None, criterion='gini',\n",
       "            max_depth=6, max_features='auto', max_leaf_nodes=None,\n",
       "            min_impurity_decrease=0.0, min_impurity_split=None,\n",
       "            min_samples_leaf=1, min_samples_split=2,\n",
       "            min_weight_fraction_leaf=0.0, n_estimators=10, n_jobs=1,\n",
       "            oob_score=False, random_state=42, verbose=0, warm_start=False)"
      ]
     },
     "execution_count": 942,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.ensemble import RandomForestClassifier\n",
    "rf=RandomForestClassifier(max_depth = 6, random_state = 42)\n",
    "rf.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 943,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>importance</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>A6</th>\n",
       "      <td>0.185223</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A5</th>\n",
       "      <td>0.179310</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A2</th>\n",
       "      <td>0.124426</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A9</th>\n",
       "      <td>0.110562</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A1</th>\n",
       "      <td>0.091137</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "    importance\n",
       "A6    0.185223\n",
       "A5    0.179310\n",
       "A2    0.124426\n",
       "A9    0.110562\n",
       "A1    0.091137"
      ]
     },
     "execution_count": 943,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "feature_importances = pd.DataFrame(rf.feature_importances_,\n",
    "                                   index = cols_input,\n",
    "                                    columns=['importance']).sort_values('importance',\n",
    "                                                                        ascending=False)\n",
    "feature_importances.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 944,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAysAAAPRCAYAAAD9XjcjAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAMTQAADE0B0s6tTgAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAIABJREFUeJzs3Xt0VPW9/vFncg8hNiFGLAIeqhJtEAwJRgiXGI2BFUaEBI9KFeUIIhYvaI3aAqKVipejYkFEjlLKqVyEAMmC0KbY1hZbBIJoTWNrpYabhBACBJLJJPv3B4f5kYIa4kz2d7Lfr7VmxeyZ2fN5xsmwn+zZOy7LsiwBAAAAgGFC7B4AAAAAAM6GsgIAAADASJQVAAAAAEairAAAAAAwEmUFAAAAgJEoKwAAAACMRFkBADhCfX29Dhw4YPcY7crr9WrPnj12jwG0ihN/RvHNKCsAAGNkZWWpb9++SklJaXFZsGDBt173bbfdpu3bt/thym+WlZWlkpKSdnmsrzNt2jQj5jhdSUmJ8vLylJKSotTUVN1xxx36y1/+YvdY3+ixxx5Tnz59WrwuU1NTdeedd+pf//pXQB5z5MiRWr16dUDWfbqkpCT169fvjJ+7devWBfyxT9eeP6MIHmF2DwAAwOmee+45DR8+3O/rPXz4sN/Xabqamhq7R2hh69atmj59uubNm6e0tDR5vV6tXr1aEydOVGFhoS655BK7R/xaN998s2bMmOH7vqamRtOnT1dBQYGWLVtm42Tf3tKlS3XllVfaOoMTf0bxzdizAgAIGvv379fUqVN1zTXXKCsrSwsWLFBzc7Mk6ciRIyooKNB1112nfv36KScnR6WlpZKkyZMna+/evXr00Uc1b948rV69WiNHjmyx7pSUFN9v+LOysjRjxgxdc801mjp1qiRp06ZNGjVqlNLS0jR27NhW/wb4scce07PPPqvbb79dV111lW666Sbt3LlTU6ZMUUpKinJzc/XJJ59IklavXq3bb79dDz/8sFJSUpSdna3169f71lVZWakpU6YoPT1dw4YN089+9jPV19dLkl599VVNmjRJbrdb11xzjR5//HFt3bpVL730kn784x9LkpYtW6Ybb7xRaWlpSk9P15NPPinLsiRJt99+u1566SXfXo/8/HyVl5f7Hvudd95RTk6OUlJSNHbsWO3cuVOS1NDQoDlz5igzM1ODBg3SY489piNHjpz1uSgrK1PPnj119dVXKyQkRBEREbrllls0fvx4HTp0SJLk8Xg0Z84cZWRkaMCAAbrvvvt8151L/r17937t68Uf4uPjlZeXp4qKCt+yX//618rPz1d6erpSU1P10EMP6cSJE5JOvhaefvpp3XHHHUpJSZHb7dbmzZt9992wYYNuuOEGpaSkaMaMGWpsbPRdd/z4cf30pz/V4MGDlZ6erh/+8Ifau3evJOkvf/mLcnNz9corryg9PV3XXHONVqxYocWLF2vw4MG6+uqr9cYbb7Q55yeffKLx48crLS1N1113nRYsWKCmpiZfpoceekjXXXedsrKydOLECf3jH//QXXfdpQEDBignJ0crV670rWvTpk3Kzc1VWlqa3G63Vq1aJenMn1HAxwIAwBDXXnuttWHDhrNe5/V6rVGjRllPP/20deLECauystIaOXKk9ctf/tKyLMuaMWOGdd9991l1dXVWY2Oj9corr1hDhw4967pXrVpl5ebmtlj/VVddZf35z3/23fbWW2+1jh07Zh05csTauXOnddVVV1mbN2+2GhsbrQ0bNlhpaWnWl19++Y05CgoKrP79+1sff/yx1dDQYP3gBz+w+vTpY23evNlqaGiwpk2bZt1zzz2+uXr37m3NmzfPamhosH7zm99YycnJ1qeffmo1NDRY1113nTVz5kzr+PHj1v79+62bb77Zmj59umVZljV37lwrOTnZ+vDDD60jR45YlmVZP/jBD6xFixZZlmVZO3bssAYMGGB9+umnlmVZVnl5udW3b19r8+bNvtsOGTLE+uyzz6y6ujrrvvvusyZMmGBZlmX98Y9/tFJSUqwPPvjAampqst566y0rIyPDamxstJ5++mnr1ltvtQ4cOGAdPXrUmjZtmjV16tSzPi8VFRVWv379rPHjx1tLliyxPv74Y6uxsbHFbf77v//bcrvdVmVlpVVfX2898MAD1tSpU885/ze9Xs5VQUGBNWvWrBbL9u3bZ91+++3Wvffea1mWZe3du9fq27evtWXLFsuyLKuystIaPHiwtWLFCt86rrrqKmvHjh1WQ0OD9dRTT1k33HCDZVmW9emnn1p9+vSxfve731kej8dauHCh1bt3b2vVqlWWZVnWI488Yv3nf/6ntX//fuv48ePW9OnTrZEjR1oej8f685//bPXu3dt65ZVXLK/Xay1btsy64oorrOnTp1sNDQ3Wpk2brMsvv9yqrq4+a7bevXtbO3fuPOt11dXVVlpamrVgwQKroaHB+sc//mFlZ2dbr7/+ui/TgAEDrC+++MI6cuSIdezYMWvw4MHWwoULLY/HY5WXl1tDhw61Nm3aZHm9Xis1NdV6//33Lcs6+brq16+fdejQIcuyvv7nH87FnhUAgFEee+wxpaWl+S633XabJOnjjz/Wrl27VFBQoKioKHXv3l2TJ0/2ffxm6tSpmj17tiIiIrRv3z7FxMToyy+/bPMcOTk5iomJUWxsrN555x2NHDlSAwcOVFhYmIYPH66+ffuqqKioVesaMmSIkpOTFRERodTUVPXp00cDBw5URESEBg4c2OIg+G7duunee+9VRESErr/+eqWnp2vDhg3atm2bDh48qCeeeELR0dHq2rWrfvSjH2nNmjW+vQWXXnqp+vbtq9jY2DNmSEpK0tq1a3XZZZfp0KFDOnr0qGJjY1s8RyNHjtT3vvc9derUScOHD9euXbskSUVFRRo5cqTS0tIUEhKiO+64Q6+++qosy9LKlSv1yCOPKDExUZ07d9Zjjz2mjRs3+vaGnK53796+j3stXbpUY8aM0cCBA/Xcc8/59iIUFRXpnnvuUffu3RUZGakZM2bohz/84Tnn/6bXS1usWLFCaWlpSklJUZ8+fXTbbbepT58+eu655yRJCQkJKi4u1oABA1RbW6uDBw8qPj6+xXM8dOhQ9evXTxERERo5cqTveJcNGzb49hiFh4fr7rvv1oUXXijp5N6rDRs26JFHHlHXrl0VHR2tH//4x6qsrNRHH30kSXK5XJo4caJCQ0M1cOBANTU16b/+678UERGhYcOGqbm5Wfv27fvKbHfccUeLn7uHH35Y0sk9IXFxcbrnnnsUERGhSy65RFOmTPHtEZGkAQMGqEePHoqNjdXvf/97derUSRMnTlR4eLguv/xyjRs3TsuWLVNoaKhiY2O1evVqbdmyRVdffbW2b9+u+Pj4Nv8/QcfHMSsAAKM8++yzZz1mZc+ePWpoaNDAgQN9yyzLUkjIyd+7HThwQLNnz9ann36qXr166cILL/R9xKktLrjgAt9/7927V3/5y1+0YcMG37Kmpib16tWrVes6fWMsNDRU5513nu/7kJCQFnN2795dLpfL9/2FF16ogwcPqrq6WomJiYqIiGhx24aGBlVXV58x878LCQnR66+/rpKSEsXFxSk5OVnNzc0tPhaVkJDg+++wsDDfXFVVVUpLS2uxrpSUFFVXV6u+vl4TJ05sMXNkZKR2796tLl26nDFHr169NH36dEnSoUOH9Ic//EFz5sxRRESEHnzwQVVVVfk20iWpS5cu6tKli4qLi88p/ze9Xk63bt06zZw50/f9G2+80SLvKaeOWWlqatLy5cv1yiuvaMiQIercubMkKTw8XKtXr9bKlSsVGRmp73//+6qvr2/x//frnuPTc7tcLl100UWSpNraWjU2Nqp79+4tnuPExETt27dP559/vqKiohQdHS1JvoynSuup77/uI3BLliw56zEr1dXVvjlO6d69u+8jaNKZz/vu3btbPH/Nzc3q0aOHJOnNN9/Uz3/+c02dOlWNjY0aO3asHn744Rb/X4HTUVYAAEGha9euiouL0/vvv+9bVltbq6NHj0qSHnroIY0ePVpLlixRSEiI/vjHP37lmbBCQkJaHA/Q0NDgO67glNM3vrt27apx48apoKDAt6yyslLf+c53WjX76ev6Jv9+6ta9e/dqwIAB+u53v6uqqip5PB7fht0XX3yh8PBw3xxf9zhvvvmmPvroI23cuNF3+8GDB7dqpgsvvFD79+/3fW9Zlp577jndeeedioiI0LJly3TZZZdJOnm65H/961+6+OKLz1jPbbfdpmuuuUb333+/pJNF5KabbtIXX3yhjz/+2PdYp++JqKys1KpVqzRkyJBzyv9Nr5fT3Xjjjbrxxhtb9VxIJwvnbbfdpoMHD2rq1KlauXKlevXqpeLiYq1Zs0bvvPOOr3jccsstrVpn165dzzgO6tRr4fzzz1dERIR2797tW++p0/yef/75Z2T3p+9+97tnnP66srJSiYmJvu///Xm//PLLW+x5qa6ultfr1fHjx7Vv3z69+OKLsixLZWVl+uEPf6ikpCSNGTMmIPMj+PExMABAUOjbt68SEhL0yiuvqKGhQYcPH9aDDz6oZ555RpJ07NgxRUZGKiQkRLt379bPf/5zSScP2JakiIgI34Zqr169VFlZqe3bt6uxsVHz58//2scePXq0Vq9erW3btsmyLG3btk2jRo0KyCl3d+3apV/96lfyer36zW9+o+3btys3N1d9+/bVRRddpNmzZ+vEiRP68ssv9cILLyg3N/crfyt9euZjx44pPDxcYWFhqq+v17x581RVVdWitH2VUaNGqbi4WGVlZWpubtbSpUu1YcMGdenSRaNHj9bzzz+vQ4cOyePx6OWXX9Ydd9whr9d7xnpyc3O1dOlSbdy4UUeOHFFjY6M++ugjFRcXKzs72/dYCxcu1L59+1RfX6+XX35Z//rXv845/ze9XvzhvvvuU69evfT444+rublZx44d8504wOv1auXKlfrwww9b9RyPHDlSW7du1caNG+X1evXLX/5SlZWVkk6W65tuukkvvPCCvvzyS504cUKzZ8/WBRdcoP79+/stz9lkZmaqrq5OCxYskMfj0T//+U+99tpruummm77y9vv379fy5cvl9Xq1f/9+3XXXXXrjjTfU1NSkKVOm+E6JfMEFF8jlcikuLk5Sy9crcAplBQAQFMLDw/X666+roqJCw4YNU05Ojrp06aJnn31WkvTMM8/o7bffVkpKiiZMmKCcnBxFRUXp73//uyRpzJgxeuaZZzRnzhz169dPd911l+6//34NHTpULpdLl1566Vc+dmpqqp5++mnNmjVLqampKigo0LRp03wb2P7Uo0cPbdu2TQMHDtTcuXM1b948XXzxxQoPD9eCBQv05ZdfKjMzU6NGjdKVV17Z4uNL/+7GG2/UkiVL9OCDD2rChAmKiYnR4MGDdd111+nzzz9XVlaW7/n5OldffbWmT5+uJ554QmlpaSopKdHChQsVHh6uxx9/XBdffLFGjx6tgQMH6sMPP9SiRYsUFRV1xnrGjRunxx9/XIsWLdKwYcM0YMAA/eQnP9HEiRM1duxYSdKkSZM0ePBg3XLLLRo6dKgkadasWeec/5teL/4QGhqqZ599Vp988ol+8YtfaMyYMerbt6+uv/56DRkyRL/97W81evRoffrpp9+4rv/4j//Q3Llz9fLLLystLU1bt25Vv379fNef+jsv+fn5Gjx4sA4cOKA333xT4eHhfstzNuedd57+53/+R5s3b9agQYM0fvx4jRw5UlOmTPna269fv16DBg3SmDFjlJqaqkcffVSxsbGaO3euFi1apP79++uWW27RrbfeqqysLEktf0aBU1zWt/lALwAA8JvVq1frzTffVHFxsd2jAIAR2LMCAAAAwEiUFQAAAABG4mNgAAAAAIzEnhUAAAAARqKsAAAAADASZQUAAACAkSgrAAAAAIwU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eu655xQXF6c5c+ZQVoAAq6qq0pYtW1RUVKTo6GhJUn19vXJzczVkyJAWx6E0NDTo8OHDkqTExEQNGTJEr732mu/6zz77TD169GjV48bExOjqq6/Wu+++q9/+9re655579Le//c13/QUXXKC9e/f6vt+zZ4/Cw8MVG/vVv/05dOiQunTpov/93/9VbW2t5s2bpyeffFIrV65s3ZMBY1iWbPmH067HNQX5ye/U/E7OLjk3f6uPWfnss880depUffrpp6qpqdHw4cM1dOjQFhsqAAJj7dq1Sk9PV8+ePZWYmKjExET16NFDmZmZvjOD/f73v1djY6Pmzp2rxsZGSdKwYcNUVlamP/3pT7IsSyUlJcrPz9fx48db/djDhw/XvHnzdPHFF+s73/lOi+tGjhypRYsWaffu3Tp27JheeOEF3XDDDQoPD//K9e3Zs0cTJ07U559/rvPOO0+dO3c+Y70AAADSOZSVqKgoVVdXq7S0VKmpqYqIiFBFRUWLj3kACIw1a9b4jjs5ndvt1rp16/TCCy/oqaee0uDBg2VZlsLDwxUeHq4uXbro1Vdf1YsvvqjU1FTNnz9f8+fPP6djzbKysrRnz54zPgImSXl5eRo5cqTGjRunzMxMde7cWbNmzfra9V155ZWaNGmSxo8fr/79++uDDz7QzJkzWz0PAABwDpdltW6H0oIFC7R06VIdO3ZM8+bN03nnnae7775b9957r+68884Ajwngq1RXV6uqqkqXX365pJMfD0tJSdH27dt9HxnriAp+/p4++fyQ3WM4UnRkmFbMztXBg+1/zMr558e2++Oagvzkd2p+J2eXOk7+sLAAH7MyefJkDRkyRJ07d9bFF1+sAwcO6KWXXtKgQYPO+UEB+M/x48d1xx13aOXKlerevbsWLVqklJSUDl1UAACAM5zTqYu7du2qoqIi7d27Vw888MA5fe4dQGD06NFDjzzyiO68807V1taqb9++mjNnztfe591339W0adPOel1SUpKWLVsWiFEBAADOSavLSllZmSZPnqwrr7xS27dv1/jx41VQUKCHH35Yt912WyBnBPANbr75Zt18882tvv21116rsrKyAE4EAADw7bX6APtnn31WTz/9tBYtWqTQ0FB1795dCxcu1OLFiwM4HgAAAACnanVZ+ec//6nrr79eknx/bTo1NVWHDnGAKwAAAAD/a3VZueiii/TBBx+0WLZ9+3ZddNFFfh8KAAAAAFp9zMr999+vyZMny+12y+Px6Pnnn9eqVav005/+NJDzAQAAAHCoVu9ZycrK0pIlSxQSEqKrr75aR44c0fz5830fDQMAAAAAfzqnPSuzZ8/Wk08+GcBxAAAAAOCkVu9Z+eCDDxQWdk5/lgUAAAAA2qzV7eOGG27Q3XffrZycHF1wwQW+M4Kdug4AAAAA/KnVZeW9996TJL311lstlrtcLsoKAAAAAL9rdVnZtGlTIOcAgHMSFRGq6Eg+mmqHTlE87wCA9tHqf3H+/W+snG7AgAF+GQYAWmvWpEF2j+BoHk+TLMvuKQAAHV2ry8qkSZNafF9fXy+Xy6VLLrlERUVFfh8MAL7O4cN18nqb7R6j3blcUkJCrKqrj9paFigqAID20OqyUlZW1uL7hoYGzZ8/X6GhoX4fCgC+iWU5e4PZ6fkBAM7Q6lMX/7vIyEhNnTpVy5cv9+c8AAAAACDpW5QVSfr4448VEvKtVgEAAAAAZ9Xqj4G53e4W3zc2Nmr37t266667/D4UAAAAALS6rEyYMKHF9yEhIerVq5f69u3r96EAAAAAoNVlZf/+/br33nvPWP7888/rRz/6kV+HAgAAAICvLStVVVW+s4C9/vrruvTSS2WddvqZo0eP6le/+hVlBUC7c7lOXpzmVGY7snP2MQBAe/vasnLeeefp9ddfV01NjRoaGvSzn/2sxfWRkZFn3dsCAIEWFxdj9wi2SkiIbffH9HiaVFt7vN0fFwDgXF9bViIjI7Vq1SpJ0uTJk7VgwYJ2GQoAvsnMhZtVvqvG7jEco1NUmBbPyJHLxR4WAED7afUxK2crKl6vV3//+991xRVX+HUoAPgm9Z4mnWjw2j0GAAAIoFaXlU2bNumpp57SgQMHWhy3EhUVdcZftwcAAACAb6vVZeX5559XXl6eYmJitHPnTo0dO1avvvqqhg8fHsj5AAAAADhUq//8/L59+3TfffcpOztb+/fvV0ZGhl544YX/x96dh1VZ5/8ffx02ISFxwa10xsklLVc2RVPBEHEp01wn03Eptcktt8zMLNM2Lctdi8kcS3NHBsW0cRtFCrPUycnMUAQBlViEw3L//vDX+UaKooLccJ6P6+LSc5/7/tzv930O55zXuRe0Zs2akqwPAAAAgJ0qclipVq2acnJyVLt2bZ0+fVqSdP/99ys5ObnEigMAAABgv4ocVry9vTVp0iRlZmaqYcOGWrZsmcLCwlStWrWSrA8AAACAnSpyWJk+fbqqVKminJwcvfjii1q/fr1WrFihadOmlWR9AAAAAOxUkU+w9/Dw0MyZMyVJVapU0fbt20uqJgAAAAAo+p4VSVq9erV69Oghf39/xcfH67nnnlNaWlpJ1QYAAADAjhU5rCxdulRr167VqFGjlJ+fLw8PD2VmZmrWrFklWR8AAAAAO1XksLJ27VotXrxYXbt2lcVikYeHh+bPn6+9e/eWZH0AAAAA7FSRw0pmZqbtyl+//QX7e+65RxaLpWQqAwAAAGDXihxWfH199c477ygvL88WUJYsWaJWrVqVWHEAAAAA7FeRw8pLL72kw4cPy8fHR+np6Wrbtq2ioqI0ffr0kqwPQBkWGhqqJ598ssC0r776Sl27dlXLli3Vq1cvHTlypJSqAwAAZnfTSxcvW7ZMzzzzjGrUqKH169fr+++/17lz51SjRg01a9ZMTk5FvvoxADty5MgReXp66sKFCzpx4oQaN26sX3/9VePHj9fSpUvl5+endevWacKECdq1a1dplwsAAEzopntWlixZ8n8zOzjorbfeUmhoqFq1akVQAVCojRs3qmPHjurRo4c+//xzSdK9996rffv2yc/PT1arVampqfL09CzlSgEAgFndNG38djL9b06ePFlixQAoH6xWqyIjI7Vx40bl5OSod+/emjJlitzc3FSxYkXFxcUpJCREDg4OWrx4cWmXi1tQmtdU+W3d9npdF/ov+K+9sef+7bl3if5vGla42heAW7Vz50499NBDql27tiSpUaNGioiIUO/evSVJtWrV0pEjR7Rjxw6NHTtWO3fuVJUqVUqzZBRR1aoepV2CKWooTfRP//bKnnuX7Ld/juMCUOw2btyo2NhYtW3bVpKUkZGh3NxcW1j57RDS7t27a+XKlTp8+LBCQkJKrV4UXUpKmv6ww/2usViuvlmXZg2lif7p3177t+fepfLTv6OjgypXrnjLy900rOTl5SkqKsp2OFhOTk6B25LUuXPnW14xgPIpKSlJ0dHR2rp1q9zc3CRJWVlZ6tatm/773/9qxowZWrt2rW1+q9UqDw/7/LaoLDIMlfqbpRlqKE30T//22r899y7Zb/83DStVq1bVnDlzbLcrV65c4LbFYiGsALDZvHmz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pUt3tHxWVpYyMzOLNO+6deu0bt26IgW9oti2bZsk6dChQ8UyHgAAQFnCnpVb1Lp1ax05csR2e9++ferVq5fc3Nz0ww8/SLq618Db21uurq6SpNjYWD322GNq2bKlJk2apJycHEnSjz/+qKefflre3t7q0aOH9uzZc911Xrp0SWPGjJG3t7eCgoIUEREh6WpQmDJlivz9/RUUFKQVK1bIMAxJUpMmTbRq1Sr5+/urffv22rNnjyZPnqyWLVuqb9++SkpKknT1G/GFCxcqICBA7dq109q1a69bw1dffaXu3bvLz89PY8eOVWpqqqxWq0aMGKG4uDi1b99ekvTTTz/p6aeflq+vr/r166eTJ0/axlizZo3atWuntm3bKioq6rrrmTp1quLj4zVs2DDt3r37htvvwoULGj16tPz8/NSjRw9FR0dfM96BAwe0dOlSbdq0SRMmTCi0F0mKi4vTwIED5ePjo27duik8PFySNHjwYOXl5ally5ZKS0u7bt2S1LZtW+Xm5mrgwIHavn27fv75Zw0dOlQBAQHy9vbWtGnTlJ+ff8uPzx/3WAQFBenAgQO220uWLNGsWbOuqaeo60hPQ/1eBwAAIABJREFUT9fUqVPVunVrhYSEKDIy8pbHkKSoqCgFBgYqKChIGzZssE0v7Dlx6NAhPfHEE+rfv78CAgKKPaQCAICyj7Byix566CFlZ2crLi5OkrR//34FBAQoICBA+/btkyR9/fXXCggIsC1z8OBBrVy5UlFRUTp8+LCioqJktVr197//XR07dtTBgwf14osvaty4cTpz5sw165wxY4ZcXV21f/9+vffee3rppZeUlJSkN954Q1euXNGuXbsUFhamtWvX2g6ZysvL0/Hjx7V//349+eSTGjlypG1drq6uBULJ3r17FRERocWLF2vOnDk6duxYgfWfOXNGEydO1MyZM7Vv3z7VrFlTM2fOlIuLi5YvX646depoz549ys3N1ahRo9SpUycdOHBAQ4YM0ciRI2W1WvX9999r3rx5WrFihf71r3/p+++/v+72nTt3rmrXrq2VK1cqMDCw0O0nSRMnTlTdunW1b98+vfzyyxo3bpwuXrxYYLyAgAA9++yz6tmzp+bNm1doL5L03nvvqU2bNoqJidHrr7+uuXPnKjc3V//4xz/k6Oio2NhYeXh4FPrc2L9/vyQpMjJSISEhmj59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FRERERERMSWVFRERERERMSWVFRERERERMSWVFRERERERMSWVFRERERERMSWVFRERERERMSWVFRERERERMSWVFRERERERMSWVFRG5KhlGTY9ARERE/mwqKyIiIiIiYkoqKyIiIiIiYkoqKyIiIiIiYkoqKyIiIiIiYkoqKyIiIiIiYkoqKyIiIiIiYkoqKyIiIiIiYkoqKyIiIiIiYkoqKyIiIiIiYkoqKyJyVXJxqekRiIiIyJ9NZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUXkImRmZl7R9Z0+fZpTp05d0XVe7hivdEYRERGRS6WyIpUaPnw48fHx9tcFBQX4+voyadIkh/m6du3Kzp07GTx4MJ9++ulfPczLlpGRga+v7wXnO3z4MMOHD7/o9aekpBAREVHhe4888gg//fQTwBXZf++//z5vvvnmJS+fk5PDfffdV61509LSGDFiBB07dqRTp04MHz6cH3744YLL7d69m7vvvhuAwsJCBg4ciJ+fHytXrrzkcYuIiEjtpLIilQoODiY1NdX+eteuXbRt25bk5GQMwwDg2LFj5Obm4u/vX1PD/MsUFBRgtVqv6Dqv9FWVvLy8y1r+zJkznD59+oLzlZe0Le5mAAAgAElEQVSX8/jjjxMZGcmePXtITk4mODiY4cOHU1paWu3tff/99/zyyy/s2bOHhx9++HKGLiIiIrWQyopUKjg4mP3799tf79ixg/vvv5969erx/fffA2evGvj7++Pu7g5Aamoq9913H35+fkycOJGysjIAfvrpJx599FH8/f2JiooiKSmpwm3m5eUxduxY/P39iYiIYOPGjcDZojB58mSCgoKIiIhg2bJl9sLk6+vLe++9R1BQEOHh4SQlJTFp0iT8/PwYMGAAJ0+eBCAiIoI333yTkJAQwsLCWLNmTYVj+OKLL+jTpw+BgYGMGzeO/Px8SktLefzxx0lPTyc8PByAI0eO8OijjxIQEEB0dLTDVYVVq1YRFhZGaGgoiYmJFW5nypQpZGZmMnz4cLZt21bl/jtx4gRjxowhMDCQqKgo9uzZc976kpOTWbp0KevWrePZZ5+tNAtA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6WmfHhoaSnZ2drXKisViYcmSJWzbto3AwEBefPFF5s2bx2233XbevNOnT+f3338nLCyMmJgY5syZQ9OmTYmNjcVisRAZGcmgQYPo27cv0dHRF52nWbNm9OzZk3HjxjFz5kxat27t8H7r1q2ZPn06EydOpFOnTmzevJm4uDjc3Nxo3bo1TZo0ITAwEIC4uDjWrl1LYGAgzz33HLNnz6ZVq1a0adOG2NhYnnzySbp3707btm0rHU9UVBTjxo274L+vMn/+fPbv309ISAjDhg1j9OjR3HXXXefNFx4ezp49exgxYkSVWWJjYzl06BBBQUE88MADDB06lPbt29OkSRP7lyhkZGRUOp7GjRvz7rvvsn//frp160ZgYCBz585lzpw53H777Vgslkr3j4iIiEh1uRiGM15QEmcUERHBK6+84vAchVy9Tp1y3mdWvLwakJNzdd+7fCmcOTsov/I7b35nzg61J7+b26U9s6IrKyIiIiIiYkp6wF5EKhQeHl7pPwy5evVq2rRp8xePSERERJyNyoo4ja1bt9b0EK4qSUlJNT0EERERcXK6DUxERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVERERERExJZUVErkqGUdMjEBERkT+byoqIiIiIiJiSyoqIiIiIiJiSyoqIiIiIiJiSyoqIiIiIiJiSyoqIiIiIiJiSyoqIiIiIiJiSyoqIiIiIiJiSyoqIiIiIiJiSyoqIiIiIiJiSyoqIXJVcXGp6BCIiIvJnU1kRERERERFTUlkRERERERFTUlkRERERERFTUlkRERERERFTUlkRERERERFTUlkRERERERFTUlkRERERERFTUlkRERERERFTUlkRERERERFTUlkRERERERFTUlkRERERERFTUlkRERERERFTUlkRp5OZmXlF13f69GlOnTp1Rdd5uWO80hmv9PpEREREqkNlpZYbPnw48fHx9tcFBQX4+voyadIkh/m6du3Kzp07GTx4MJ9++ulfPczLlpGRga+v7wXnO3z4MMOHD7/o9aekpBAREVHhe4888gg//fQTwBXZf++//z5vvvnmJS+fk5PDfffdV+35t2zZwgMPPICfnx+hoaFMnjyZrKysCsfzySefMHTo0Esem4iIiMjF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8MADDB06lPbt29OkSRP7lyhkZGRUOaYHHniA2bNnEx8fT3BwMH369CE/P5+PP/7YfhvcH8dTlf79+xMWFkb//v0JDw/HMAymTZt23nwWi4X58+ezYMEC/Pz8mDFjBq+//rrKioiIiJzHxTCc8YKSXK0iIiJ45ZVXHJ4zEed06pTzPrPi5dWAnJyr+97lS+HM2UH5ld958ztzdqg9+d3cLu2ZFV1ZERERERERU9ID9iK1WHh4eKX/MOTq1atp06bNXzwiERERkepTWZGrytatW2t6CFeVpKSkmh6CiIiIyCXTbWAiIiIiImJKKisiIiIiImJKKisiIiIiImJKKisiIiIiImJKKisiIiIiImJKKisiIiIiImJKKisiIiIiImJKKisiIiIiImJKKisiIiIiImJKKisiclUyjJoegYiIiPzZVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSUVFZERERERMSU3Gp6ACIil6JOHef+XYsz53fm7KD8yu+8+Z05O1z9+S91/C6GYRhXeCwiIiIiIiKX7equaCIiIiIiUmuprIiIiIiIiCmprIiIiIiIiCmprIiIiIiIiCmprIiIiIiIiCmprIiIiIiIiCmprIiIiIiIiCmprIiIiIiIiCmprIiIiIiIiCmprIiIiIiIiCmprIhIjdm3bx9RUVF06NCBxx57jJycnPPmOX36NOPGjaNjx45ERETwn//8x/7eyZMneeyxx/Dz8+Pee+8lNTXV/l5aWhoDBgygQ4cO9O/f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GMb/XSsVERERERExEd0GJiIiIiIipqSyIiIiIiIipqSyIiIiIiIipqSyIiIiIiIipqSyIiIiIiIipqSyIiIiIldEenp6TQ9BRGoZlRUREZGr2ODBg4mPj6/pYfDyyy/zr3/9q6aH4WD37t0MHjyYjh070rFjR/r378+WLVtqelgichHcanoAIiIicvXLy8vj2muvrelh2P3666+MHDmSl19+mcjISAC++OILJkyYgIeHByEhITU8QhGpDpUVERGRWmLRokWkp6dTXFzMjh07aNKkCbNnz+aTTz7h888/x9PTk5kzZxIWFsbu3buZNm0aXbp04eOPP6Z+/fo8/vjjDB48GIDc3FxeeeUVkpKScHV1JTw8nMmTJ+Pp6cknn3zCmjVrcHFxIS0tjUcffZT169fj4uLCL7/8wvLly9myZQtvvfUW6enpWK1WwsPDeemll6hXrx5Tpkyhfv36/Pjjjxw4cIDmzZszdepUe4HYunUrCxYsID09nRtvvJFJkyYRHh5OeXk58fHxrFmzhoKCAvz9/XnhhRfw9vY+b18cPHgQDw8PunfvTp06dQDo3r0748aNo6ioCADDMHj77bf54IMP+P3337nzzjuZOXMmN99880Xlf+utt2jZsiVz585l+/btuLi40Lt3byZMmIDFYvmLjr5I7aTbwERERGqRhIQEBgwYwL59+2jfvj1DhgwhKCiI3bt306tXL15++WX7vL/88gtnzpwhOTmZBQsWMH/+fLZv3w7A008/TWFhIZs3b2bjxo2cOnWKmJgY+7KpqakMHz6cbdu2MXr0aKKiohgwYADLly/n+PHjTJw4kcmTJ7N7924+/fRTUlJSSEhIsC//ySefMGHCBHbv3k1gYCAzZswAIC0tjXHjxvH000+TkpLC2LFjefrpp8nLy+Pdd9/lf//3f4mPjycpKYlbbrmFJ598EsMwztsPgYGBlJeXEx0dTXx8PKmpqZSWljJs2DDuvvtuAD766CNWrlzJkiVL2LNnD7fffjvPPvvsRee/8847mTx5MkVFRWzatIlPP/2U7777jtdff/0KHlkR56QrKyIiIrXIHXfcwV133QWc/cC+e/du+vbtC0BYWBirVq2yz2uxWJgyZQrXXHMNHTt2JCoqioSEBG655Rb27dvHl19+ScOGDQGYNm0aXbt2JTs7G4DrrruO7t27VziGxo0bk5CQQIsWLcjPzycnJ4frr7/evixAeHg47du3B6BPnz6sXLkSgI0bNxIYGGgvFD169MDb25t69eqxZs0axowZw8033wzAs88+S0BAAAcPHuTOO+90GIOXlxfr1q3jvffeY926dcybNw93d3fuvfdepk6dioeHB+vXr+fhhx/m9ttvB2DcuHH89NNPpKenX1T+nJwctm3bRlJSEg0aNADgmWee4bHHHmPy5MkXeQRF5I9UVkRERGqR66+/3v7nOnXqcN1119lfu7q6OlyFaNKkicNzJj4+Puzbt4+cnBzc3Nzw8fGxv9esWTPc3Nw4fvw4AE2bNq10DHXr1uWTTz7ho48+4pprrsHX15czZ844bLtx48b2P7u5udnfO3nyJM2aNXNY37lSk5mZybRp0+xXYQBsNhvHjh07r6wAeHt7ExMTQ0xMDAUFBXz11VfMmzePGTNmMG/ePE6ePOmQ8dprr6Vdu3akpqZeVP7MzEwA7r33XoftW61WcnNzHbKKyMVRWREREalFXFxcqj1vXl4eZWVl1K1bFzj7odvHx4cbbrgBq9XK8ePH7cXh2LFjWK1WvLy8OHLkSJXbSUhIYN26daxdu9b+gX/gwIHVGpOPjw9ff/21w7TFixdzzz334O3tzXPPPUfXrl3t76WlpdG8efPz1jNx4kRcXV3tt701aNCAHj16UFBQwPLly+3bysrKsi9TWFjIokWLGDZs2EXl9/b2xsXFhS+++AIPDw8AiouLOXHiBI0aNapWbhGpmJ5ZERERcVKnT59m4cKFlJaWsm/fPjZs2EC/fv3w9vYmNDSUWbNmkZ+fT35+PrNmzSIgIKDCYgBnbykrKCgAzn7od3V1xWKxYLVa+eijj/jmm28oKyu74Jh69+7N3r172bp1KzabjX//+98sX74cT09PHnjgAd544w2OHTuGzWZj5cqV9OvXj1OnTlW4nk2bNvHRRx/x22+/YbPZSEtLY82aNfbbt/7xj3+watUqfvrpJ6xWK4sXLyY1NfWi85+b/6WXXqKwsJDTp0/zwgsvMHbs2IsqjyJyPl1ZERERcVL16tWjuLiYu+66i+uuu44ZM2bQqVMnAF599VXmzp1L7969KS0tpUuXLsyePbvSdfXq1Yvx48fTv39/3n//ffbs2UP37t255ppraN++Pf369eOHH3644JhuueUWFi1axPz584mJieHmm28mLi6Oxo0bM3z4cKxWK48++ih5eXm0bNmSpUuXVvhtYN26dWPhwoXEx8fz8ssvU1ZWRrNmzbj//vsZMWIEAH379uW3335j5MiR5Ofn07FjR/7nf/7nkvLPmzePl19+mZ49e1JSUkLHjh1ZvHjxBfOKSNVcjIq+QkNERERqtd27dzNq1ChSU1NreigiIpXSbWAiIiIiImJKKisiIiIiImJKug1MRERERERMSVdWRERERETElFRWRERERETElFRWRERERETElFRWRERERETElFRWRERERETElFRWRERERETElFRWRERERETElP4/v2YrwzXxYcYAAAAASUVORK5CYII=\n",
      "text/plain": [
       "<Figure size 640x1200 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "num = np.min([50, len(cols_input)])\n",
    "ylocs = np.arange(num)\n",
    "# get the feature importance for top num and sort in reverse order\n",
    "values_to_plot = feature_importances.iloc[:num].values.ravel()[::-1]\n",
    "feature_labels = list(feature_importances.iloc[:num].index)[::-1]\n",
    "\n",
    "plt.figure(num=None, figsize=(8, 15), dpi=80, facecolor='w', edgecolor='k');\n",
    "plt.barh(ylocs, values_to_plot, align = 'center')\n",
    "plt.ylabel('Features')\n",
    "plt.xlabel('Importance Score')\n",
    "plt.title('Feature Importance Score - Random Forest')\n",
    "plt.yticks(ylocs, feature_labels)\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 4: Briefly discuss any observations you have of the feature importances. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "In feature importance it is observed that the question A9 is a positive important feature using logistic regression.Question A9 is as follows 'Does your child use simple gestures? (e.g. wave goodbye) '. It is a important feature as the gestures of the child can be a determining factor that the toddler has Autism or not. \n",
    "The Question A6 which is 'Does your child follow where youâ€™re looking? ' is positive important feature using random forest. The child's eyesight can be a important factor for detection of ASD."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Hyperparameter tuning"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 4: Using RandomizedSearchCV, optimize a few of your baseline models. \n",
    "    Note that GradientBoosting Classifier may take a while so you might need to adjust the number of iterations or specific parameters. If this takes too long on your computer, feel free to take that one out. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 945,
   "metadata": {},
   "outputs": [],
   "source": [
    "# train a model for each max_depth in a list. Store the auc for the training and validation set\n",
    "\n",
    "# max depths\n",
    "max_depths = np.arange(2,20,2)\n",
    "\n",
    "train_aucs = np.zeros(len(max_depths))\n",
    "valid_aucs = np.zeros(len(max_depths))\n",
    "\n",
    "for jj in range(len(max_depths)):\n",
    "    max_depth = max_depths[jj]\n",
    "\n",
    "    # fit model\n",
    "    rf=RandomForestClassifier(n_estimators = 100, max_depth = max_depth, random_state = 42)\n",
    "    rf.fit(X_train_tf, y_train)        \n",
    "    # get predictions\n",
    "    y_train_preds = rf.predict_proba(X_train_tf)[:,1]\n",
    "    y_valid_preds = rf.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "    # calculate auc\n",
    "    auc_train = roc_auc_score(y_train, y_train_preds)\n",
    "    auc_valid = roc_auc_score(y_valid, y_valid_preds)\n",
    "\n",
    "    # save aucs\n",
    "    train_aucs[jj] = auc_train\n",
    "    valid_aucs[jj] = auc_valid"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 946,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAZYAAAEPCAYAAABhkeIdAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAIABJREFUeJzt3XlYlXX+//HnWVlEBOEAbilukYprGi5h1owLiltq7pVLNc1UmpY0ozOTVmrTDDOlv74zZWGmjWlmoeK4lOaCGmWRCLlilgKHTXbOdv/+wI6ioh7kcA7wflxXV577Pvc5r4PIi/u+P/fnVimKoiCEEELUELWrAwghhKhfpFiEEELUKCkWIYQQNUqKRQghRI2SYhFCCFGjpFiEEELUKCkWIYQQNUqKRQghRI2SYhFCCFGjpFiEEELUKCkWIYQQNUqKRQghRI2SYhFCCFGjtK4OUNvy8oqx2Ryf0DkgwIecnCInJLozkssxkssxkssx9TGXWq3C37+RQ9s0uGKx2ZRqFcuv27ojyeUYyeUYyeUYySWHwoQQQtQwKRYhhBA1SopFCCFEjXJ6sRQVFTFixAh+/vnn69alpqYyduxYhgwZwp/+9CcsFgsAFy5cYMqUKQwdOpTf/e53FBcXA1BQUMATTzzBsGHDmDJlCkaj0dnxhRBCOEjlzHvef//99yxcuJCzZ8+yfft2WrZsWWn9iBEjeOWVV+jevTt//OMf6dKlC5MnT+bJJ59k5MiRDB8+nJUrV1JSUsILL7zA4sWLCQkJ4YknnmDz5s3s2bOHf/7znw5lyskpqtZJLIOhMUZjocPbOZu75UpMyWDT3tPkFpTT1NeDsQPb0bdziKtjSS7JJbmqmUutVhEQ4OPQNk4tlj/96U+MGTOGF198kQ8++KBSsfzyyy88+uij7Nq1C4CkpCTefPNNVq1axX333ceRI0fQarVcvHiRqVOnsnv3bh588EHWrl1Ls2bNsFgs9OnTh8OHD6PT6W47kxSL8ySmZLA6IQ2TxWZfptOqmfybDvS5J9hluY6kZrJu10nMkktyNfBceq2aR4eFOVQu1SkWpw43fvXVV6tcl5WVhcFgsD82GAxkZmaSl5eHj48PWq220vJrt9Fqtfj4+JCbm0twsOv+8sQVm/aerlQqAGaLjdXbf2T19h9dlOrGJJdjJJdj3DWXyWJj097TTt+bctl1LDabDZVKZX+sKAoqlcr+/6td+/jqbdRqx04TOdq8VzMYGld7W2dyl1w5BeVVrps5snMtJqls1ecpVa6TXNeTXI6pa7lyC8qd/jPDZcUSEhJS6eR7dnY2QUFBNG3alMLCQqxWKxqNBqPRSFBQEABBQUFkZ2cTEhKCxWKhuLgYPz8/h95XDoU5x9ETVQ+kCPD1oH8n1+1Vbt5z6oalJ7luTHI5pq7laurr4dDPjOocCnPZcOMWLVrg4eHBN998A8Bnn31GZGQkOp2Oe++9l23btgGwefNmIiMjARg4cCCbN28GYNu2bdx7770OnV8RNU9RFHYc+YkVm34gsIkHOm3lbym9Vs3Yge1clK7C2IHt0Euu2ya5HCO5rqf561//+ldnv8nq1asZM2YMvr6+zJ49m9DQUIKDg+nZsyeLFy/mvffew9/fn3nz5qHRaOjZsyf/+te/ePfddyksLOQvf/kLnp6edO/enQ8//JC3336bEydO8Oqrr+Lr6+tQltJSE9UZrtCokQclJSbHN3QyV+ay2mx8uPMkWxLP0etuA/Mn9iC4qTfnMgooK7cS4OvBpN90dPnomFZBPgQ08ZRckktyVSOXSqXC21vv2DbOHBXmjuRQWM0oKbPw9mfHSDmbS1REa8YObIv6qnNh8vVyjORyjORyzJ3kcrtRYaJ+yr5Uyr82JJORW8Jjw8KI7Nbc1ZGEEG5EikU45MyFAt78JBmzxcbcCd3o1KapqyMJIdyMFIu4bUlpWbyz5ThNGul5cVIPmgc6do8GIUTDIMUibklRFBIO/8TGPadp36IJf3g4HF8HT+YJIRoOKRZxUxarjTX/+5F9yRfpc08QM4ffg06rcXUsIYQbk2IRVSouM/P/Pj1G6rk8ovu1YfT9oVXOgiCEEL+SYhE3lJVfyr82fE9WXikzh99D//Bmro4khKgjpFjEdU79fIk3P0lGURTmT+zO3Xf5uzqSEKIOkWIRlRw6nsF7W9MI8PVgzvhuBDf1dnUkIUQdI8UigIqRX1sOpvPpvrN0bOXHH8aG4+Ml87AJIRwnxSIwW2zEJaSRmJJB384hPDYs7LrJJIUQ4nZJsTRwRaVmVmz6gRPn8xlzfygj+rWRkV9CiDsixdKAZeSW8M8N35NbUM4TIzsR0cn19+gWQtR9UiwN1I8/5bFi0w+oVCpemNSdDi0du2GaEEJURYqlATrww0XiEtII8vfiuXFdCfKXkV9CiJojxdKAKIrC5n1niT+Yzj2t/Xl6TBcaecrILyFEzZJiaSDMFiurtqZyJDWLAV2bMX3I3Wg1MvJLCFHzpFgagIISE299kszpXwoY90A7ht13l4z8EkI4jRRLPXchu5h/bvieS8Umnh7dhXvDglwdSQhRz0mx1GPH03NZ+ekxdFo1Cyb3pG1zX1dHEkI0AFIs9dRX319gzf9+JKSpN8+N70pgEy9XRxJCNBBSLPWMTVH4ZO9pEg79ROfQpvxuVBe8PeWvWQhRe+QnTj1Sbrby7pbjfPOjkQd6tGDKbzugUcvILyFE7ZJiqScuFZXz5ic/kH6xgIkPtue3vVvJyC8hhEtIsdRRiSkZbNp7mtyCcnwb6bFYrZitCn8YG06PjgZXxxNCNGBOPU4SHx9PVFQUgwcPZu3atdet37t3L9HR0URHRzNv3jyKi4sBSE9PZ+rUqURHRzNt2jTOnj1r3+a1115j+PDhjBgxgi1btjgzvttKTMlgdUIaOQXlKMClYhPFZVaGR7SWUhFCuJzTiiUzM5PY2FjWrVvH5s2bWb9+PadOnbKvLygoICYmhtjYWOLj4wkLCyM2NhaAl156ibFjxxIfH8+8efOYM2cOAImJiSQnJ/P5558TFxfHyy+/TGlpqbM+gtvatPc0JovtuuVffX/BBWmEEKIypxXLwYMHiYiIwM/PD29vb4YMGcL27dvt69PT02nevDnt27cHYNCgQezatQuA1NRUhg4dCkD37t3Jysri/PnzWK1WysvLsVgslJaWotfrnRXfreUUlDu0XAghapPTiiUrKwuD4cphmaCgIDIzM+2P27RpQ0ZGBmlpaQAkJCSQnZ0NQKdOndi6dStQsZeSn5+P0WhkwIABtGrVisjISKKionjiiSfw8mp412cE+Ho4tFwIIWqT007e22y2SqOSFEWp9NjX15fly5ezaNEibDYbEyZMQKermGl32bJlLFmyhDVr1hAZGUlYWBg6nY7169ej0WjYv38/+fn5TJ8+nW7dutG9e/fbzhUQ4FPtz2QwNK72tjXpsRGdif3oKDZFsS/z0Gl4bERnt8kI7vP1upbkcozkcozkcmKxhISEkJSUZH9sNBoJCroyT5XVaiUkJIQNGzYAkJycTKtWrQCwWCysXLkSvV6P2Wxm/fr1tGzZkrfeeotJkyah0+kwGAw88MADJCUlOVQsOTlF2GzKrZ94DYOhMUZjocPbOUNokA8KCp56DeUmK019PRg7sB2d7/Jzm4zu9PW6muRyjORyTH3MpVarHP6F3GmHwvr160diYiK5ubmUlpayY8cOIiMj7etVKhUzZswgMzMTRVGIi4sjKioKgNjYWHbv3g3Axo0bCQ8Px9/fn7CwMPt5mJKSEg4dOkSXLl2c9RHc1jc/ZqEoMH9iDz7/+yj+9nR/+naW2woLIdyD04olODiYuXPnMn36dEaPHs2IESPo2rUrs2fP5ocffkCtVrN48WJmzZrF0KFD8fX1ZebMmQDMnz+f1atXM3z4cHbu3MnSpUsBeOqpp7BYLAwbNowJEyYwatQoIiIinPUR3Nah45kE+XsR2sw9d7mFEA2bSlEUx48L1WF1/VBYbkEZL/y/g4wcEMqoAaFuk+takssxkssxkssx9eZQmHCOw6mZKEBE52BXRxFCiBuSYqljEo9l0q65L8H+3q6OIoQQNyTFUof8nFXEz8YiIuREvRDCjUmx1CGJxzNQq1T0vkduLyyEcF9SLHWETVE4lJJJl7ZN8fVumFPZCCHqBimWOuLET/nkFZbL9SpCCLcnxVJHJKZk4KHX0L1DoKujCCHETUmx1AFmi5WkH4306mjAQ6dxdRwhhLgpKZY64PtTOZSWW+QwmBCiTpBiqQMSUzJo0kjPPa39XR1FCCFuSYrFzRWVmkk+ncN9nYJRq1W33kAIIVxMisXNJf2YhdWmyGEwIUSdIcXi5g4dy6BZgDd3BVf/BmVCCFGbpFjcWHZ+KSd+vkTfziGV7r4phBDuTIrFjR06nglARCeZyVgIUXdIsbgpRVFITMmgQ8smBPp5uTqOEELcNikWN/VTZhEXc0rkpL0Qos6RYnFTiSkZaNQq7g2TmYyFEHWLFIsbstkUDh/PpGu7AHy8dK6OI4QQDpFicUOp5/K4VGySw2BCiDpJisUNHUrJwMtDQ7f2Aa6OIoQQDpNicTPlZitJJ4zce3cQOq3MZCyEqHukWNzMdyezKTdZ5TCYEKLOkmJxM4kpGfg39qDjXX6ujiKEENUixeJGCkpMpJzNJaJTMGqZwkUIUUc5tVji4+OJiopi8ODBrF279rr1e/fuJTo6mujoaObNm0dxcTEA6enpTJ06lejoaKZNm8bZs2eBiqvRV65cyejRoxkyZAibN292Zvxa93WqzGQshKj7nFYsmZmZxMbGsm7dOjZv3sz69es5deqUfX1BQQExMTHExsYSHx9PWFgYsbGxALz00kuMHTuW+Ph45s2bx5w5cwD4/PPPOXjwIB9//DEffvghr7/+OgUFBc76CLXuUEoGLQ0+tAySmYyFEHWX04rl4MGDRERE4Ofnh7e3N0OGDGH79u329enp6TRv3pz27dsDMGjQIHbt2gVAamoqQ4cOBaB79+5kZWVx/vx5EhISmDFjBnq9HoPBwLp16/D09HTWR6hVmXklnL5QQN/OMuGkEKJu0zrrhbOysjAYDPbHQUFBJCcn2x+3adOGjIwM0tLSCAsLIyEhgezsbAA6derE1q1bGT9+PImJieTn52M0Gjl37hynT59m9erVFBYWMnv2bNq0aeNQroCA6u8NGAyNq73trew6egGVCoYNaIfB37FJJ52Z605ILsdILsdILsfUZi6nFYvNZqt0DxFFUSo99vX1Zfny5SxatAibzcaECRPQ6SqmL1m2bBlLlixhzZo1REZGEhYWhk6nw2q18uOPP7Jq1Sqys7OZNGkSnTp1cqhccnKKsNkUhz+PwdAYo7HQ4e1uh6Io7D5yjrtb+YHF4tD7ODPXnZBcjpFcjpFcjrmTXGq1yuFfyJ1WLCEhISQlJdkfG41GgoKuTKhotVoJCQlhw4YNACQnJ9OqVSsALBYLK1euRK/XYzabWb9+PS1btiQwMJChQ4ei0+lo1qwZ3bp14/jx4w7vtbibsxcLycwrJSqitaujCCHEHXPaOZZ+/fqRmJhIbm4upaWl7Nixg8jISPt6lUrFjBkzyMzMRFEU4uLiiIqKAiA2Npbdu3cDsHHjRsLDw/H392fQoEEkJCSgKAp5eXkkJydzzz33OOsj1JrElAy0GjW97paZjIUQdZ/TiiU4OJi5c+cyffp0Ro8ezYgRI+jatSuzZ8/mhx9+QK1Ws3jxYmbNmsXQoUPx9fVl5syZAMyfP5/Vq1czfPhwdu7cydKlSwF47LHHCAwMZMSIEUyaNImnn36a0NBQZ32EWmGx2jiSmkn39gF4ezptB1IIIWqNSlEUx0841GHudo4l+XQO/9zwPc+MDadHR8OtN6ilXHdKcjlGcjlGcjmmts+xyJX3LnYoJYNGnlrC28lMxkKI+kGKxYVKyy18e8JI73uC0Wrkr0IIUT/ITzMXOnrSiMliI6KTXBQphKg/pFhc6FBKJoFNPGnfsomrowghRI2RYnGRS0XlpKTnEtFZZjIWQtQvUiwucjg1C0WBiE4yk7EQon6RYnGRxJQMWgc3pnlgI1dHEUKIGiXF4gIXc4o5l1EoMxkLIeolKRYXSEzJRKWCPjIaTAhRD0mx1DJFUTiUkkGnNk3x8/FwdRwhhKhxUiy17NQvl8i+VCbXrggh6i0pllqWmJKJXqumZzXmBRNCiLpAiqUWWaw2vk7NpEdHA14eMpOxEKJ+kmKpRT+cyaG4zCKjwYQQ9ZoUSy1KTMnEx0tHpzZNXR1FCCGc5qbF8sknn5CcnGx//Prrr/Ppp586PVR9VFJm4buT2dwnMxkLIeq5Kn/Cbdy4kX//+9/odDr7sl69evH222+zefPmWglXn3xzIguL1UZEFzkMJoSo36oslnXr1hEXF1fpnvIPPfQQq1at4oMPPqiVcPXJoZRMgvy9aNvM19VRhBDCqaosFkVRaN68+XXLW7VqhdVqdWqo+ia3oIy0c3lEdApGJTMZCyHquSqLxWq1YrPZrltus9mwWCxODVXfHE7NRAH6dpaZjIUQ9V+VxdKnTx/i4uKuW/7+++8THh7uzEz1zqGUTNo29yW4qberowghhNNVeZXec889x9SpU9m1axc9e/bEZrPx3XffUVRUdMPCETf2c1YR57OKmPLbjq6OIoQQtaLKYmncuDEbNmxg69atpKSkoFKpmDJlCoMHD640UkzcXOLxDNQqFb3DglwdRQghasVN5xXR6/WMGTOGMWPG1FaeesWmKBxKyaRL26b4NtK7Oo4QQtSKKotl2rRplUYwaTQa/Pz8GDhwIKNHj66VcHXdiZ/yySssZ/ygdq6OIoQQtabKYpk6dWqlxzabjZycHNasWUNeXh6PP/74LV88Pj6et99+G4vFwqOPPsqUKVMqrd+7dy9vvPEGAB07dmTx4sU0atSI9PR0Fi5cyKVLl/Dz82Px4sWEhobat7NYLEyZMoVHHnmEsWPHOvSBa9Oh4xl46DX06CAzGQshGo4qi2XIkCE3XB4dHc20adNuWSyZmZnExsayadMm9Ho9EydO5L777qN9+/YAFBQUEBMTw5o1a2jfvj3vvPMOsbGxLFy4kJdeeonx48czduxYvvvuO+bMmcNnn31mf+2VK1eSnp5ejY9be8wWK1+nGenV0YCHTuPqOEIIUWscnrSqSZMmt3WR38GDB4mIiMDPzw9vb2+GDBnC9u3b7evT09Np3ry5vWgGDRrErl27AEhNTWXo0KEAdO/enaysLM6fPw/At99+S1paGoMGDXI0eq36/lQOpeUWImQmYyFEA+PwTUEURbmtCySzsrIwGK4cAgoKCqo0oWWbNm3IyMggLS2NsLAwEhISyM7OBqBTp05s3bqV8ePHk5iYSH5+PkajEX9/f5YuXcrbb79tP4TmqIAAn2ptB2AwNL7t53675Tj+jT2I7HUXGidPOulIrtokuRwjuRwjuRxTm7mqLJb8/PwbLluzZg3du3e/5QvbbLZKezaKolR67Ovry/Lly1m0aBE2m40JEybYhzEvW7aMJUuWsGbNGiIjIwkLC0On0/Hyyy/z5JNPEhgY6NCHvFpOThE2m+LwdgZDY4zGwtt6blGpmaTUTB7s2ZLc3GKH38tZuWqT5HKM5HKM5HLMneRSq1UO/0JeZbFERESgUqlQlIofwiqVCn9/fwYOHMif/vSnW75wSEgISUlJ9sdGo5GgoCvXclitVkJCQtiwYQMAycnJtGrVCqg4Ob9y5Ur0ej1ms5n169fTtGlTEhMTOXHiBG+99RYXL17k0KFDaLVaRo4c6dCHdrakH7OwWBWZwkUI0SBVWSxpaWnXLbNYLGzfvp3HH3/cXghV6devH2+99Ra5ubl4eXmxY8cOlixZYl+vUqmYMWMGGzZsICgoiLi4OKKiogCIjY0lKiqKYcOGsXHjRsLDw2nRogX79++3bx8TE0OfPn3crlQADh3LoFmAN3cFV/+wmxBC1FW3dY7l0qVLrF+/nrVr11JSUnLdUOQbCQ4OZu7cuUyfPh2z2cy4cePo2rUrs2fP5tlnnyU8PJzFixcza9YsTCYTffv2ZebMmQDMnz+fBQsWsGLFCoKDg1m6dOmdfcpalH2plBM/X2JMZFuZyVgI0SCplF+Pdd3AmTNnWL16NZ9//jktWrTAaDSya9cuGjd2z5NTt8PZ51i2Jqbzyd4zLH+qLwY/r2okdE6u2ia5HCO5HCO5HFPb51iqHK70xBNPMHXqVHQ6HR988AFbtmyhUaNGdbpUnE1RFA4ey6BDyya1UipCCOGOqiyW48eP07lzZzp06EDr1q0B5NDOLfyUWcTFnBIi5KS9EKIBq7JY9uzZw5gxY9iyZQsDBgzg2Wefpby8vDaz1TmJKRlo1DKTsRCiYauyWLRaLVFRUaxZs4ZNmzYRFBREeXk5gwcP5qOPPqrNjHWCzaZwODWTru0C8PGS2woIIRqu27okvH379ixcuJCvvvqKmTNn8vHHHzs7V52T+lMel4pMcu2KEKLBc2iuES8vLx555BE+/fRTZ+Wpsw4dy8DLQ0O39gGujiKEEC7l3EmsGohys5WkE0Z63R2ETiszGQshGjYplhrw3clsyk1WOQwmhBBIsdSIQykZ+Df24O67/FwdRQghXE6K5Q4VlJg4djaX+zoFo5brfIQQQorlTn2dmoXVJjMZCyHEr6RY7tChlAxaGhrRKkhmMhZCCJBiuSNZeSWcvlAgeytCCHEVKZY7cCglExVwXye5r70QQvxKiqWaFEUhMSWDu+/yo6mvp6vjCCGE25BiqaazFwvJzCuVmYyFEOIaUizVlJiSgVaj5t67Da6OIoQQbkWKpRosVhtHUjPp3j4Ab0+ZyVgIIa4mxVINx9PzKCwxy2EwIYS4ASmWajiUkkEjTy3hbWUmYyGEuJYUi4PKTBa+PWmkd1gQOq18+YQQ4lryk9FBR09kYzLb5DCYEEJUQYrFQYkpGQT4etK+ZRNXRxFCCLckxeKAS0XlpKTnEtFZZjIWQoiqSLE44HBqFoqCHAYTQoibcGqxxMfHExUVxeDBg1m7du116/fu3Ut0dDTR0dHMmzeP4uJiANLT05k6dSrR0dFMmzaNs2fPAlBcXMxzzz1n32br1q3OjH+dQykZtA5uTIvARrX6vkIIUZc4rVgyMzOJjY1l3bp1bN68mfXr13Pq1Cn7+oKCAmJiYoiNjSU+Pp6wsDBiY2MBeOmllxg7dizx8fHMmzePOXPmAPCf//yH5s2bEx8fT1xcHEuXLiU7O9tZH6GS85mFpGcUEtFZJpwUQoibcVqxHDx4kIiICPz8/PD29mbIkCFs377dvj49PZ3mzZvTvn17AAYNGsSuXbsASE1NZejQoQB0796drKwszp8/T58+fZg2bRoAAQEB+Pn51Vqx7P32Z1Qq6HOPFIsQQtyM1lkvnJWVhcFwZR6toKAgkpOT7Y/btGlDRkYGaWlphIWFkZCQYC+JTp06sXXrVsaPH09iYiL5+fkYjUb69+9v337btm2YTCZ7Md2ugADHbsi155vzfLAtFWN+KTqtmgt5pXRsG+jQazibwdDY1RFuSHI5RnI5RnI5pjZzOa1YbDYbqqtGTimKUumxr68vy5cvZ9GiRdhsNiZMmIBOVzHv1rJly1iyZAlr1qwhMjKSsLAw+zqAhIQEXnvtNd599120Wsc+Qk5OETabclvPTUzJYHVCGiaLDQCzxcZbH39HQWGZ29zcy2BojNFY6OoY15FcjpFcjpFcjrmTXGq1yuFfyJ1WLCEhISQlJdkfG41GgoKC7I+tVishISFs2LABgOTkZFq1agWAxWJh5cqV6PV6zGYz69evp2XLlgCsWbOGVatWsWrVKu6++25nxQdg097T9lL5lcliY9Pe025TLEII4W6cdo6lX79+JCYmkpubS2lpKTt27CAyMtK+XqVSMWPGDDIzM1EUhbi4OKKiogCIjY1l9+7dAGzcuJHw8HD8/f3ZtWsXcXFxfPTRR04vFYCcgnKHltcm08mDFK2bx5lXx1G0bh6mkwddHUkIIQAnFktwcDBz585l+vTpjB49mhEjRtC1a1dmz57NDz/8gFqtZvHixcyaNYuhQ4fi6+vLzJkzAZg/fz6rV69m+PDh7Ny5k6VLlwLw5ptvUl5ezlNPPcWoUaMYNWoUP/zwg7M+AgG+Hg4try2mkwcp3xeHUpQDKChFOZTvi5NyEUK4BZWiKLd3wqGeuJNzLAB6rZpHh4W59FBY0bp5l0ulMpVnY7zH/AWVT1NUKtde+1ofjzU7k+RyjORyTL05x1If/Foem/aeJregnKa+Howd2M7l51duVCoASlkhxR/NB60Hav/mFf/5tUBz+c+qxoEuLxwhRP0nxXILfTuH0LdziFv9JqLy9kcpybt+uZcv+nvHYsv7BVveBaw/p2A5ceDKEzR61P7NUPs1R+3fArV/czT+zVE1DkKllsIRQtQMKZY6RlEU8PSBa4tFq0cfMRF9h36Vn19ejC3/ItbLZWPL+wXrxR+xnEq88iSNFrVfM9R+LS7v6VTs5ah8g1CpNbXwqYQQ9YkUSx1jObEfJfc8mvZ9sWWcQCnKReXTFH3vh68rFQCVRyM0we3RBFe+kFQxlWLLv1CxZ/PrHk7WKSynD115klqLukmIvWzsh9d8g1FpbvytYzp5ENPXn1B4i1xCiPpLiqUOsRXlUHZwHZqQjngNmo1Kpa72ITqV3gtNUDs0Qe3QXbVcMZdhy794Ze8m7wJW41ksZ74GLg96UGlQNwm+rnCsxnTKD6wBi6nitS6PVgOkXIRoQKRY6ghFUSj76n1QrHg+MMtpJ+FVOk80hlA0htDK728px5afYT9/Y8v7BWvueSzp38DNBhZaTJiObJRiEaIBkWKpI8xpe7H+fAyP/tNQ+wbdeoMaptJ6oAlsjSawdaXlisWE7VImtrxfKPvi/264rVKcS9F/F1wenXbVITW/Zqi0rr0mSAhR86RY6gBboZHyQ/9F0/wedJ0GuTpOJSqtHk1AKzQBrSg/suHGQ6F1XmgC78KW9wuWn5JBsf66NarGgZdHp10ZOKD2a4ZK51mrn0MIUXO1BpGZAAAeKUlEQVSkWNycotgo2/seAJ4DZ7r1dSj63g9XnFO5fI4FAK0ejwHT7IfCFJsF26WsikNq+Rew5Vb83/RzCtgs9s1UPgFXDYm+XDp+zVHpvWr5UwkhHCXF4ubMx7/AeiEVj/sfQ93Yvabrv9av5WH6+pMqR6up1Fo0l6+fuZpis6IUGC+PUPvFPmLNfCEVs9V8ZftGTSsNGtD4Xb740+Pmd/WU0WpC1B4pFjdmK8ii/PDHaFp2QRc20NVxbou+Qz/0Hfo5PFpNpdag8gtB7RcCob3syxWbDaXQWDEcOv/KwAHz8S/BemXPSOXtd9X5myulo/L0sc+tJqPVhKgdUixuSlFslO15F9QaPCNnVLqXTUOiUqtRNQlG3SQYLT3syxXFhlKYgy3/F6y5F7BdLh1z2ldguTL7tMrLF8VUAlZL5Re2mDB9/YkUixBOIMXipszHdmLNOIHnwJmofZq6Oo7bUanUqHwNqH0NaO/qbl+uKDaU4rzL524ul82P+274GkpRznU3oBNC3DkpFjdky79I+ZGNaO7qhrbjAFfHqVNUKnXFiX+fALirKwCWX45XOXFn8Ufz0Ybei65tb9RBbd16cIQQdYUUi5tRbDZK97wLWj2ekY/Lb9M14Iaj1TQ6tB0HoBTnYk7ZjfmH/6Fq1BRtaC+0bXujCW4vJeOG3HUQhuSqTIrFzZiSt2PLOo3ng0+i9vZzdZx64Vaj1RRTCZZz32E58zXm1C8xH9uJytvvcsn0QRPcQWZ/dgPuOghDcl1PisWNWPN+wZS0CW2bXmjbRbg6Tr1ys9FqKr03ug790HXoh2IqxfLT9xUlk/YV5pTdqLx80YbeW7EnE9JRZnx2EdORDZX3OgEsJsr3rcZ28UfXhALMpw7VqVy1MWhFisVNKDYrZXveRaX3wuP+R+UQmIuo9F7o2kegax+BYi7D8lMyljNHMP+4H/PxL1B5Nq7YkwntjaZ5mJSMkyjmMqzZ57AZz2A1pmM1nkUpvv4eRABYyrH89H3tBrzm/ata7o65qjrfWJOkWNyE6but2Ixn8fzN06i9fF0dR1AxIaeuXR907fqgmMuxnE+u2JM5mYg5dQ8qDx+0oT0rDpc1D0Olln9O1aFYzdhyzmM1nsFqPIvNmI4t/4J9clOVTwCawDZYyorAVHLd9iqfAHwm/722Y9tVeatwN87lbPIvwQ1Yc85j+vYztG37oGvbx9VxxA2odB7o2vZG17Y3iqUcy/ljFSVz+kjFtTMejdC16VmxJ9OiU5X3q2noFJu14mJX4xlsxrNYjenYcs+DrWL+OJWXL2pDKPrQe9EEhaIODEXt3QS4/pwBUHGDu94Pu+CTXFHVVEYNOZd897uYYrVQtucdVB6N8BgwzdVxxG1QaT3QhfZCF9oLxWLC8vPlkjmTVHHNjN4bbZse6EJ7o2nZGZVGd+sXrYcUxYZyKavSnog1+9yVGRP0XmgMoejDh6A2hKIJaouqUdMqDwPfzpRBriC5rqdSlJvdTKP+yckpwmZz/CM765735UmfYvr2MzwHP4OuTa9bb1BLue5UQ8ylWM1Yf07BfPZrLOnfgqkUdF5oW3dH17ZPRclo9bWe607cbi5FUVCKc7Fm/bonchZrdnrF1wBAo0cT2LqiQAxt0BjaomoSVO0h3XX961Xb7iSXWq0iIMDHoW1kj8WFrNnpmI5uQdu+b7VKRbgXlUaHtnV3tK27o1gtWH85jvnM11jOfYvlVCLoPCvWh/ZG2yoclVZfZ69/sJUWVJxYz6ooEVt2OkppQcVKtQZ101bo2kWgvlwiav/mMtChAZFicRHFaqbsy3dReTXGs/9UV8cRNUyl0aK9qyvau7qi2B7F+ksqlrNfYzn7LZZTh0Drgcq/BUrOT/bbBbj19Q9fvYfl3HeobNbLI7RyLz9bVTHhZ6uu9juPqpu2rHLPTDQMUiwuYvrmM2x5P+M1dM4tp3wXdZtKrUXbKhxtq3CUAdOxXvjx8nUye4FrDstaTJTvfQ9L6h5XRAXAmnWm0r1xKhZasJ45gso3CE1Ih4oCMYSiCWwtN2UT13FqscTHx/P2229jsVh49NFHmTJlSqX1e/fu5Y033gCgY8eOLF68mEaNGpGens7ChQu5dOkSfn5+LF68mNDQUBRF4fXXX+fLL79ErVazZMkSevWqe4eQrFlnMH2/FW3H+ytNoCjqP5Vai7ZlZ7QtO2NO23PjJ9ks4MrDRteWylV8Jr5ei0FEXeW0YsnMzCQ2NpZNmzah1+uZOHEi9913H+3btwegoKCAmJgY1qxZQ/v27XnnnXeIjY1l4cKFvPTSS4wfP56xY8fy3XffMWfOHD777DP+97//cfr0abZt28a5c+d48skn2bZtG1pt3dnxUiymilFg3v549pvk6jjChVQ+AVVeZ+A9YoELElVw5fUP7kJRFPLyjJhMZVy3V3kTWVlqbDab84JV061zqdDrPfH3N9TIxdlO+4l88OBBIiIi8POrmO9qyJAhbN++nT/84Q8ApKen07x5c3vRDBo0iFmzZrFw4UJSU1MZOnQoAN27dycrK4vz58+zd+9eoqKiUKvVhIaG0qxZM44ePUrv3r2d9TFqXHnSJmz5F/GKmo9K7+3qOMKF5PoH91VUdAmVSkVwcEuHRq5ptWosFvcrllvlUhQb+fnZFBVdonHjO5+j0GnFkpWVhcFgsD8OCgoiOTnZ/rhNmzZkZGSQlpZGWFgYCQkJZGdnA9CpUye2bt3K+PHjSUxMJD8/H6PRSFZWFkFBQfbXMBgMZGRkOJTL0WFzVzMYGld7W4Cyn9MoTP4fjXsMxtCj7x291tXuNJezSK5bMAyh0NeLvC/XYinIQesbgP+gKTTuEim5boMz/x5zci4QEBBcraMhWq17Tlh681xq/P0DyM3NxGBodefvdcevUAWbzVZpl+raGyr5+vqyfPlyFi1ahM1mY8KECeh0FReSLVu2jCVLlrBmzRoiIyMJCwtDp9Pd8DXVDs4666rrWBRLOcWb30TVOACl25gaG+teH8fNO5Pb5QrugdfEHvZcZUCZO+Rz11yXOfvv0Ww2oyiO733U1T0WAEVRYzKZr/u6utV1LCEhISQlJdkfG43GSnsbVquVkJAQNmzYAEBycjKtWlU0pcViYeXKlej1esxmM+vXr6dly5aEhISQlZVlf43s7OxKr+nOyo9sRLmUideIBaj0Xq6OI4S4hYY2EWxNfl6n7bP169ePxMREcnNzKS0tZceOHURGXtmVVqlUzJgxg8zMTBRFIS4ujqioKABiY2PZvXs3ABs3biQ8PBx/f38iIyOJj4/HarVy7tw50tPTCQ8Pd9ZHqDGWC2mYj+1E1/khtM3vcXUcIUQdUlRUxEsvzb/t56elHWfZsiVOTHRrTttjCQ4OZu7cuUyfPh2z2cy4cePo2rUrs2fP5tlnnyU8PJzFixcza9YsTCYTffv2ZebMmQDMnz+fBQsWsGLFCoKDg1m6dCkAQ4cOJTk5mZEjRwLw6quv4unp3mPoFXMZZXtXofINwqPPBFfHEUI4SWJKBpu+OkPOpTICfD0YO7AdfTuH3PHrFhYWcPLk7d/XJSysEzExne74fe+EzBV2m6p7TLds/weYj3+JV3QM2mZ3O7y9s3I5m+RyjORyjLNzZWScIySk9W0/PzElg9UJaZiuOo+h16p5dFjYHZfLggVzOXw4kb59B3Du3FmaNPHDw8ODV199naVLl2A0ZpGdbeTee/sQE7OIo0e/4b33/sOKFf/hD394gk6dOpOc/B15eXnMmfMCffv2d+hzu9U5FgGWn1MwH/8CXfgQp5SKEML5Dvxwkf3JF2/6nNMXLmGxVv6F1WSx8f62VL767kKV2w3o2oz+4c1u+tpz5rzAM888ybPPPs/48SPZsOEtmjVrzs6d2+nQoSOvvLIcs9nM1Knj+fHHtOu2N5stvPvuavbs2cM777x902KpKVIsTqKYSin76j1UTULwaEDj/4VoiK4tlVstry5//6Y0a9YcgN/+dijHjx/j44/XkZ5+lkuXLlFaev2N0O67r+LShrZt21FYWFCjeaoixeIk5Yc+QinOxXvkn2RCPiHqsP7ht96reOH/HSCn4PpbAQf4erBgSs8ay+Lh4WH/88aN/2XPni8YOXIM48b14ezZ09zozIZeX/HzR6VS3XC9M7jnlTx1nOV8Mua0r9B3HYYmuL2r4wghnGzswHbor7kAUa9VM3Zguzt+bY1Gg9VqvW75118fZuTIsQwePAyTycTJkyfcZjoZ2WOpYUp5MWVfvY/avzn6XqNdHUcIUQt+PUHvjFFhTZsGEBwcwmuvvVxp+YQJk3njjaV8+OH7NGrkQ5cuXbl48QItWrS84/e8UzIq7Dbd7iiU0j3vYDmZiPfoRWgModWJ6JRctU1yOUZyOcbdRoX9qi5feQ81NypMDoXVIEv6USwnDqDvPrxWSkUIIdyRFEsNUcqKKNsXh7ppK/Q9R7k6jhBCuIwUSw0pO/ghSlkRng/MQqWRU1dCiIZLiqUGmM8mYTl1CH3PkWgCHT8uK4QQ9YkUyx2ylRZQvm816sDW6HsMd3UcIYRwOSmWO6AoCuX7P0AxleL5wGxUajkEJoQQUix3wHLmCJazSejvHY2mqevHjgshhDuQYqkmW0k+Zfs/QG1oi77rMFfHEUIIXn31r2zbFk92tpH585+94XMGDLjX6Tnk2E01KIpC+b7VYCnHc9AsVGqNqyMJIVzMdPIgxV9/gq0oB5VPAPreD6Pv0M8lWQIDDbzxxpsueW+QPZZqsZw8iOXcUTx6P4zGr7mr4wghXMx08iDl++KwFeUAoBTlUL4vDtPJg3f82n/84wvs2bPb/njGjKkcPfoNv/vdTGbMmML48aPYt29PpW0uXrzAuHHR9j8/8cQMHntsMn/722t3nOd2yB6Lg2zFeZQdXIsmuAO6LkNcHUcI4WTmEwcw//jVTZ9jzTwNNkvlhRYT5Xvfw5K2t8rtdHdHout48/ujDBkSxc6dCTzwwEOcP/8TJpOJTz5ZT0zMIlq3bsM333zNv/71Bvff/8ANt4+NfZ3hw6MZPnwU27dv5bPPNt30/WqC7LE4QFEUyr56H6wWPB+YiUotXz4hBNeXyq2WO6BfvwEcO/YDJSXF7Nr1P4YMGcaiRUs4c+YUcXHv8t//fkhpaWmV2x89+g2/+c1gAAYPHoZW6/z9CdljcYDlx31Yzyfj0W8K6iZ3PmupEML96Tr2v+VeRdG6eSiXD4NdTeUTgHf0S3f2/jod/fvfz/79X/HFFzv529/+xe9/P5uePXvRo0cvevXqzcsvL7zJK6hQlIoJKFUqFepaOCcsv3LfgunkQYrWzePMqw9T9tX7qJo0Q9f5IVfHEkK4EX3vh+HaG/pp9RXLa8CQIVH8978f0qSJH97e3pw/f46ZM58iIqI/+/btvel9WO69tw/bt28DYO/eLzCZrr8hWU2TYrmJX0/IXflNREEpysZ86pBLcwkh3Iu+Qz887n8MtU8AULGn4nH/YzU2Kqxr1+4UFRUxePAwfH2bMGLEKKZNm8CUKeMoKSmhrKysysNhzz//Il9+uZtHH51EYuIBvL0b1Uimm5H7sdzEzXZvfSb/vaajVUtDvV9GdUkuxzTUXHI/livkfiw17EalcrPlQgghpFhuSnV5t/Z2lwshhHByscTHxxMVFcXgwYNZu3btdev37t1LdHQ00dHRzJs3j+LiYgAuXbrE7NmzGTlyJOPGjSM1NdW+zWuvvcbw4cMZMWIEW7ZscWZ8p5+QE0KI+shpxZKZmUlsbCzr1q1j8+bNrF+/nlOnTtnXFxQUEBMTQ2xsLPHx8YSFhREbGwvA+++/T8eOHfn88895+umnWbx4MQCJiYkkJyfz+eefExcXx8svv3zT8dt36tcTchV7KKoaPyEnhHBfDez0c41+XqcVy8GDB4mIiMDPr2J43JAhQ9i+fbt9fXp6Os2bN6d9+/YADBo0iF27dgFgs9nsey+lpaV4enoCYLVaKS8vx2KxUFpail5/zd6EE+g79MNn8t9p+6eN+Ez+u5SKEA2AVqunuLigwZSLoigUFxegvfYITTU57QLJrKwsDAaD/XFQUBDJycn2x23atCEjI4O0tDTCwsJISEggOzsbgBkzZvDII48wYMAAiouLee+99wAYMGAAH3/8MZGRkZSUlDB//ny8vLyc9RGEEA2Uv7+BvDwjRUX5Dm2nVqtvek2Jq9xOLq1Wj7+/4abPuV1OKxabzYZKpbI/VhSl0mNfX1+WL1/OokWLsNlsTJgwAZ1OB8CSJUuYMmUK06dP5+jRo8ydO5etW7eyZcsWNBoN+/fvJz8/n+nTp9OtWze6d+9+27kcHTZ3NYOhcbW3dSbJ5RjJ5ZiGmiskxN+pr1+fOa1YQkJCSEpKsj82Go0EBQXZH1utVkJCQtiwYQMAycnJtGrVCoDdu3fbz6v06NGDgIAATp8+ze7du5k0aRI6nQ6DwcADDzxAUlKSQ8XiyHUsV2uo4/mrS3I5RnI5RnI55k5yudV1LP369SMxMZHc3FxKS0vZsWMHkZGR9vUqlYoZM2aQmZmJoijExcURFRUFQFhYmP18S3p6OllZWYSGhlZaXlJSwqFDh+jSpYuzPoIQQohqcNoeS3BwMHPnzmX69OmYzWbGjRtH165dmT17Ns8++yzh4eEsXryYWbNmYTKZ6Nu3LzNnzgRg2bJl/PnPf+add95Br9ezfPlyGjduzFNPPcXLL7/MsGHD0Gg0jBs3joiICIdyqdWqWz/JCds6k+RyjORyjORyTH3LVZ3tGtyULkIIIZxLrrwXQghRo6RYhBBC1CgpFiGEEDVKikUIIUSNkmIRQghRo6RYhBBC1CgpFiGEEDVKikUIIUSNkmIRQghRo6RYbmHFihUMHz6c4cOH8/rrr7s6znWWL19OTEyMq2PYffHFF4wdO5Zhw4bxyiuvuDqO3WeffWb/e1y+fLmr41BUVMSIESP4+eefgYr7F0VHRzN48GD7De/cIdf69esZMWIE0dHRvPTSS5hMJrfI9asPP/yQadOmuSQTXJ/r6NGjTJgwgeHDh/P888+7zddr//79jBw5khEjRvDiiy86P5ciqnTgwAHlkUceUcrLyxWTyaRMnz5d2bFjh6tj2R08eFC57777lAULFrg6iqIoivLTTz8pAwYMUC5evKiYTCZl0qRJyp49e1wdSykpKVF69+6t5OTkKGazWRk3bpxy4MABl+X57rvvlBEjRiidO3dWzp8/r5SWlioDBw5UfvrpJ8VsNiszZsxwydft2lxnzpxRfvvb3yqFhYWKzWZTXnzxReX99993ea5fnTx5Urn//vuVqVOn1nqmG+UqLCxU+vfvr6SmpiqKoihz585V1q5d6/JciqIokZGRyqlTpxRFUZRnnnlG+fjjj52aQfZYbsJgMBATE4Ner0en09GuXTsuXLjg6lgA5OfnExsby1NPPeXqKHY7d+4kKiqKkJAQdDodsbGxdOvWzdWxsFqt2Gw2SktLsVgsWCwWPDw8XJbn448/5i9/+Yv9NhLJycm0bt2aVq1aodVqiY6OrnS3VVfl0uv1/OUvf8HHxweVSkXHjh1d8v1/bS4Ak8nEn//8Z5599tlaz1NVrgMHDtC9e3fCwsIAWLhwIb/97W9dngsq/g0UFRXZ78Lr7O9/p81uXB906NDB/uf09HQSEhL46KOPXJjoij//+c/MnTuXixcvujqK3blz59DpdDz11FNcvHiRBx54gDlz5rg6Fj4+Pjz33HMMGzYMLy8vevfuTc+ePV2W59VXX630+EZ3W83MzKztWNflatGiBS1atAAgNzeXtWvXsnTpUpfnAvj73//Oww8/TMuWLWs9z6+uzXXu3Dm8vb2ZO3cuZ86coWfPni45TH2jr9df//pXpk2bho+PDy1btmTo0KFOzSB7LLfh5MmTzJgxgxdffJE2bdq4Og4bNmygWbNm9O3b19VRKrFarSQmJvLaa6+xfv16kpOT+fTTT10di7S0ND755BO+/PJL9u3bh1qtZtWqVa6OZXeru626WmZmJo8++igPP/ww9913n6vjcODAAS5evMjDDz/s6iiVWK1W9u/fz/PPP8+mTZsoLS3lP//5j6tjYTQaeeONN9iyZQv79++nW7duTv8FQYrlFr755hsee+wx5s2bx5gxY1wdB4Bt27Zx4MABRo0axZtvvskXX3zBa6+95upYBAYG0rdvX5o2bYqnpye/+c1vSE5OdnUs9u/fT9++fQkICECv1zN27FiOHDni6lh2ISEhGI1G++Nr77bqSqdPn2bixImMGTOG3//+966OA8CWLVs4efIko0aNYuHChRw7dswt9owDAwPp1q0brVq1QqPRMGzYMLf4/k9KSqJjx47cddddqNVqJkyY4PTvfzkUdhMXL17k97//PbGxsW61d/D+++/b/7xp0yaOHDnCH//4RxcmqjBo0CAWLFhAQUEBjRo1Yt++fTz00EOujkVYWBh/+9vfKCkpwcvLiy+++ILw8HBXx7Lr1q0bZ8+e5dy5c7Rs2ZItW7a4xW/jRUVFzJw5kzlz5jB69GhXx7G7+rftw4cPs2LFCv75z3+6MFGFAQMG8NZbb3Hx4kWaNWvGl19+SefOnV0di44dO7J8+XKys7MJDAxk9+7dTv/+l2K5iVWrVlFeXs6yZcvsyyZOnMikSZNcmMp9devWjVmzZjF58mTMZjP9+/d3ix+QAwYM4Pjx44wdOxadTkd4eDhPPPGEq2PZeXh4sGzZMp555hnKy8sZOHCg04+B346NGzeSnZ3N+++/b/9l5sEHH+S5555zcTL31KxZMxYvXsxTTz1FeXk599xzDwsWLHB1LNq1a8dzzz3H9OnT0Wg0tG7dmsWLFzv1PeUOkkIIIWqUnGMRQghRo6RYhBBC1CgpFiGEEDVKikUIIUSNkmIRQghRo6RYhHAzubm53H333Xf0GitWrGDXrl0AxMTEuNVMA6L+k2IRoh46fPgwFovF1TFEAyUXSApxjcOHD/OPf/yDZs2acfbsWby8vHjiiSdYs2YNZ8+eZfDgwcTExPDaa6/x/fffU1xcjKIovPLKK/To0YPHH3+czp078+KLL3Lw4EFiYmLYtGkTgYGBVb7njh07iI2NxcvLiy5dulRat2HDBj766CNsNht+fn4sWrSIdu3aERMTg4eHB2lpaeTk5NC/f38WLlzIxx9/zLFjx3j99dfRaDRAxX1CJk6cSHZ2Nh06dODvf/873t7eTv06igbMqZPyC1EHHTp0SLnnnnuUlJQURVEUZebMmfb78uTk5CidO3dWkpKSlGeeeUaxWq2KoijKv//9b+XJJ59UFEVRMjMzlX79+ik7d+5U7r//fuXIkSM3fT+j0aj06tVLOXnypKIoivJ///d/SseOHRVFUZTDhw8rkydPVkpKShRFUZR9+/YpQ4cOVRRFURYsWKCMHj1aKSoqUsrLy5UpU6Yoa9asURRFUaZOnaokJCTYnzdu3DilpKREsVgsypgxY5RPP/20Jr9kQlQieyxC3EDLli3p1KkTAHfddReNGzdGr9fTtGlTGjVqROPGjZkzZw7//e9/OX/+PIcPH6ZRo0ZAxbT3S5Ys4emnn+aZZ56hd+/eN32vb775ho4dO9K+fXsAHnnkEf7xj38AsGfPHs6dO8fEiRPtzy8oKCA/Px+AMWPG2N931KhR7N69m6lTp173Hr/5zW/w8vICKm4HkZubeydfHiFuSopFiBvQ6/WVHmu1lf+pJCYm8uGHH/L444/z0EMP0bZtWz7//HP7+lOnThEYGHjbs9sqV82sdPV72Ww2Ro0axQsvvGB/nJWVRZMmTQDsh7p+fQ21+sanTa9+TZVKVen9hKhpcvJeiGr48ssvGTRoEJMnT6ZLly7s2rULq9UKVNwR8oMPPuCTTz6hsLCQ1atX3/S1evfuzalTp0hLSwMqZqz+1YABA9i6dStZWVkAfPTRRzz66KP29QkJCZhMJsrLy/n0008ZNGgQUFE4cvJeuIrssQhRDX/84x958cUXiY6OxmKx0L9/f3bs2EFhYSHPP/88CxcuJDg4mGXLljF+/Hh69+5tP7R2raZNm/LGG28wf/58dDpdpUNnAwYMYPbs2cyYMQOVSoWPjw8rVqyw3wjM09OTyZMnU1BQwJAhQ+yzST/44IP84x//wGw2O/+LIcQ1ZHZjIeqomJgYOnTowMyZM10dRYhKZI9FiFrw7rvvEh8ff8N1M2fOZOTIkbWcSAjnkT0WIYQQNUpO3gshhKhRUixCCCFqlBSLEEKIGiXFIoQQokZJsQghhKhRUixCCCFq1P8H+mTgePCFg70AAAAASUVORK5CYII=\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "import matplotlib.pyplot as plt\n",
    "\n",
    "plt.plot(max_depths, train_aucs,'o-',label = 'train')\n",
    "plt.plot(max_depths, valid_aucs,'o-',label = 'valid')\n",
    "\n",
    "plt.xlabel('max_depth')\n",
    "plt.ylabel('AUC')\n",
    "plt.legend()\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 947,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "{'bootstrap': True,\n",
       " 'class_weight': None,\n",
       " 'criterion': 'gini',\n",
       " 'max_depth': 18,\n",
       " 'max_features': 'auto',\n",
       " 'max_leaf_nodes': None,\n",
       " 'min_impurity_decrease': 0.0,\n",
       " 'min_impurity_split': None,\n",
       " 'min_samples_leaf': 1,\n",
       " 'min_samples_split': 2,\n",
       " 'min_weight_fraction_leaf': 0.0,\n",
       " 'n_estimators': 100,\n",
       " 'n_jobs': 1,\n",
       " 'oob_score': False,\n",
       " 'random_state': 42,\n",
       " 'verbose': 0,\n",
       " 'warm_start': False}"
      ]
     },
     "execution_count": 947,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "rf.get_params()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 948,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "{'n_estimators': range(200, 1000, 200), 'max_features': ['auto', 'sqrt'], 'max_depth': range(2, 20, 2), 'min_samples_split': range(2, 10, 2), 'criterion': ['gini', 'entropy']}\n"
     ]
    }
   ],
   "source": [
    "from sklearn.model_selection import RandomizedSearchCV\n",
    "\n",
    "# number of trees\n",
    "n_estimators = range(200,1000,200)\n",
    "# maximum number of features to use at each split\n",
    "max_features = ['auto','sqrt']\n",
    "# maximum depth of the tree\n",
    "max_depth = range(2,20,2)\n",
    "# minimum number of samples to split a node\n",
    "min_samples_split = range(2,10,2)\n",
    "# criterion for evaluating a split\n",
    "criterion = ['gini','entropy']\n",
    "\n",
    "# random grid\n",
    "\n",
    "random_grid = {'n_estimators':n_estimators,\n",
    "              'max_features':max_features,\n",
    "              'max_depth':max_depth,\n",
    "              'min_samples_split':min_samples_split,\n",
    "              'criterion':criterion}\n",
    "\n",
    "print(random_grid)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 949,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.metrics import make_scorer, roc_auc_score\n",
    "auc_scoring = make_scorer(roc_auc_score)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 950,
   "metadata": {},
   "outputs": [],
   "source": [
    "# create a baseline model\n",
    "rf = RandomForestClassifier()\n",
    "\n",
    "# create the randomized search cross-validation\n",
    "rf_random = RandomizedSearchCV(estimator = rf, param_distributions = random_grid, \n",
    "                               n_iter = 20, cv = 2, \n",
    "                               scoring=auc_scoring,verbose = 1, random_state = 42)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 951,
   "metadata": {},
   "outputs": [],
   "source": [
    "import time"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 952,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Fitting 2 folds for each of 20 candidates, totalling 40 fits\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "[Parallel(n_jobs=1)]: Done  40 out of  40 | elapsed:   19.2s finished\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "20.014477729797363\n"
     ]
    }
   ],
   "source": [
    "import time\n",
    "# fit the random search model (this will take a few minutes)\n",
    "t1 = time.time()\n",
    "rf_random.fit(X_train_tf, y_train)\n",
    "t2 = time.time()\n",
    "print(t2-t1)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 4: Make a plot comparing the performance of the optimized models to the baseline models. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 953,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "{'n_estimators': 800,\n",
       " 'min_samples_split': 2,\n",
       " 'max_features': 'auto',\n",
       " 'max_depth': 18,\n",
       " 'criterion': 'gini'}"
      ]
     },
     "execution_count": 953,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Your code here\n",
    "rf_random.best_params_"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 954,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Baseline Random Forest\n",
      "Training AUC:0.999\n",
      "Validation AUC:0.984\n",
      "Optimized Random Forest\n",
      "Training AUC:1.000\n",
      "Validation AUC:0.993\n"
     ]
    }
   ],
   "source": [
    "rf=RandomForestClassifier(max_depth = 6, random_state = 42)\n",
    "rf.fit(X_train_tf, y_train)\n",
    "\n",
    "y_train_preds = rf.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = rf.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "thresh = 0.5\n",
    "\n",
    "print('Baseline Random Forest')\n",
    "rf_train_base_auc = roc_auc_score(y_train, y_train_preds)\n",
    "rf_valid_base_auc = roc_auc_score(y_valid, y_valid_preds)\n",
    "\n",
    "print('Training AUC:%.3f'%(rf_train_base_auc))\n",
    "print('Validation AUC:%.3f'%(rf_valid_base_auc))\n",
    "\n",
    "print('Optimized Random Forest')\n",
    "y_train_preds_random = rf_random.best_estimator_.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds_random = rf_random.best_estimator_.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "rf_train_opt_auc = roc_auc_score(y_train, y_train_preds_random)\n",
    "rf_valid_opt_auc = roc_auc_score(y_valid, y_valid_preds_random)\n",
    "\n",
    "print('Training AUC:%.3f'%(rf_train_opt_auc))\n",
    "print('Validation AUC:%.3f'%(rf_valid_opt_auc))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 955,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\sklearn\\linear_model\\stochastic_gradient.py:128: FutureWarning: max_iter and tol parameters have been added in <class 'sklearn.linear_model.stochastic_gradient.SGDClassifier'> in 0.19. If both are left unset, they default to max_iter=5 and tol=None. If tol is not None, max_iter defaults to max_iter=1000. From 0.21, default max_iter will be 1000, and default tol will be 1e-3.\n",
      "  \"and default tol will be 1e-3.\" % type(self), FutureWarning)\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "SGDClassifier(alpha=0.1, average=False, class_weight=None, epsilon=0.1,\n",
       "       eta0=0.0, fit_intercept=True, l1_ratio=0.15,\n",
       "       learning_rate='optimal', loss='log', max_iter=None, n_iter=None,\n",
       "       n_jobs=1, penalty='l2', power_t=0.5, random_state=42, shuffle=True,\n",
       "       tol=None, verbose=0, warm_start=False)"
      ]
     },
     "execution_count": 955,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.linear_model import SGDClassifier\n",
    "sgdc=SGDClassifier(loss = 'log',alpha = 0.1,random_state = 42)\n",
    "sgdc.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 956,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "0.6602284908294678\n"
     ]
    }
   ],
   "source": [
    "penalty = ['none','l2','l1']\n",
    "max_iter = range(200,1000,200)\n",
    "alpha = [0.001,0.003,0.01,0.03,0.1,0.3]\n",
    "random_grid_sgdc = {'penalty':penalty,\n",
    "              'max_iter':max_iter,\n",
    "              'alpha':alpha}\n",
    "# create the randomized search cross-validation\n",
    "sgdc_random = RandomizedSearchCV(estimator = sgdc, param_distributions = random_grid_sgdc, n_iter = 20, cv = 2, scoring=auc_scoring,verbose = 0, random_state = 42)\n",
    "\n",
    "t1 = time.time()\n",
    "sgdc_random.fit(X_train_tf, y_train)\n",
    "t2 = time.time()\n",
    "print(t2-t1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 957,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "{'penalty': 'l2', 'max_iter': 400, 'alpha': 0.001}"
      ]
     },
     "execution_count": 957,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "sgdc_random.best_params_"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 958,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Baseline sgdc\n",
      "Training AUC:1.000\n",
      "Validation AUC:0.999\n",
      "Optimized sgdc\n",
      "Training AUC:1.000\n",
      "Validation AUC:1.000\n"
     ]
    }
   ],
   "source": [
    "y_train_preds = sgdc.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = sgdc.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "thresh = 0.5\n",
    "\n",
    "print('Baseline sgdc')\n",
    "sgdc_train_base_auc = roc_auc_score(y_train, y_train_preds)\n",
    "sgdc_valid_base_auc = roc_auc_score(y_valid, y_valid_preds)\n",
    "\n",
    "print('Training AUC:%.3f'%(sgdc_train_base_auc))\n",
    "print('Validation AUC:%.3f'%(sgdc_valid_base_auc))\n",
    "\n",
    "print('Optimized sgdc')\n",
    "y_train_preds_random = sgdc_random.best_estimator_.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds_random = sgdc_random.best_estimator_.predict_proba(X_valid_tf)[:,1]\n",
    "sgdc_train_opt_auc = roc_auc_score(y_train, y_train_preds_random)\n",
    "sgdc_valid_opt_auc = roc_auc_score(y_valid, y_valid_preds_random)\n",
    "\n",
    "print('Training AUC:%.3f'%(sgdc_train_opt_auc))\n",
    "print('Validation AUC:%.3f'%(sgdc_valid_opt_auc))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 959,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "GradientBoostingClassifier(criterion='friedman_mse', init=None,\n",
       "              learning_rate=1.0, loss='deviance', max_depth=3,\n",
       "              max_features=None, max_leaf_nodes=None,\n",
       "              min_impurity_decrease=0.0, min_impurity_split=None,\n",
       "              min_samples_leaf=1, min_samples_split=2,\n",
       "              min_weight_fraction_leaf=0.0, n_estimators=100,\n",
       "              presort='auto', random_state=42, subsample=1.0, verbose=0,\n",
       "              warm_start=False)"
      ]
     },
     "execution_count": 959,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.ensemble import GradientBoostingClassifier\n",
    "gbc =GradientBoostingClassifier(n_estimators=100, learning_rate=1.0,\n",
    "     max_depth=3, random_state=42)\n",
    "gbc.fit(X_train_tf, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 960,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "1.6426472663879395\n"
     ]
    }
   ],
   "source": [
    "# number of trees\n",
    "n_estimators = range(50,200,50)\n",
    "\n",
    "# maximum depth of the tree\n",
    "max_depth = range(1,5,1)\n",
    "\n",
    "# learning rate\n",
    "learning_rate = [0.001,0.01,0.1]\n",
    "\n",
    "# random grid\n",
    "\n",
    "random_grid_gbc = {'n_estimators':n_estimators,\n",
    "              'max_depth':max_depth,\n",
    "              'learning_rate':learning_rate}\n",
    "\n",
    "# create the randomized search cross-validation\n",
    "gbc_random = RandomizedSearchCV(estimator = gbc, param_distributions = random_grid_gbc, n_iter = 20, cv = 2, scoring=auc_scoring,verbose = 0, random_state = 42)\n",
    "\n",
    "t1 = time.time()\n",
    "gbc_random.fit(X_train_tf, y_train)\n",
    "t2 = time.time()\n",
    "print(t2-t1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 961,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "{'n_estimators': 150, 'max_depth': 1, 'learning_rate': 0.1}"
      ]
     },
     "execution_count": 961,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "gbc_random.best_params_"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 962,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Baseline gbc\n",
      "Training AUC:1.000\n",
      "Validation AUC:0.991\n",
      "Optimized gbc\n",
      "Training AUC:1.000\n",
      "Validation AUC:1.000\n"
     ]
    }
   ],
   "source": [
    "y_train_preds = gbc.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = gbc.predict_proba(X_valid_tf)[:,1]\n",
    "\n",
    "thresh = 0.5\n",
    "\n",
    "print('Baseline gbc')\n",
    "gbc_train_base_auc = roc_auc_score(y_train, y_train_preds)\n",
    "gbc_valid_base_auc = roc_auc_score(y_valid, y_valid_preds)\n",
    "\n",
    "print('Training AUC:%.3f'%(gbc_train_base_auc))\n",
    "print('Validation AUC:%.3f'%(gbc_valid_base_auc))\n",
    "print('Optimized gbc')\n",
    "y_train_preds_random = gbc_random.best_estimator_.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds_random = gbc_random.best_estimator_.predict_proba(X_valid_tf)[:,1]\n",
    "gbc_train_opt_auc = roc_auc_score(y_train, y_train_preds_random)\n",
    "gbc_valid_opt_auc = roc_auc_score(y_valid, y_valid_preds_random)\n",
    "\n",
    "print('Training AUC:%.3f'%(gbc_train_opt_auc))\n",
    "print('Validation AUC:%.3f'%(gbc_valid_opt_auc))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Pick your best model"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 4: Pick your best model. Explain why you picked it. Save the model using pickle."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 963,
   "metadata": {},
   "outputs": [],
   "source": [
    "df_results = pd.DataFrame({'classifier':['SGD','SGD','RF','RF','GB','GB'],\n",
    "                           'data_set':['baseline','optimized']*3,\n",
    "                          'auc':[sgdc_valid_base_auc,sgdc_valid_opt_auc,\n",
    "                                 rf_valid_base_auc,rf_valid_opt_auc,\n",
    "                                 gbc_valid_base_auc,gbc_valid_opt_auc],\n",
    "                          })"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 964,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>classifier</th>\n",
       "      <th>data_set</th>\n",
       "      <th>auc</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>SGD</td>\n",
       "      <td>baseline</td>\n",
       "      <td>0.999074</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>SGD</td>\n",
       "      <td>optimized</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>RF</td>\n",
       "      <td>baseline</td>\n",
       "      <td>0.984074</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>RF</td>\n",
       "      <td>optimized</td>\n",
       "      <td>0.992963</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>GB</td>\n",
       "      <td>baseline</td>\n",
       "      <td>0.991481</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>GB</td>\n",
       "      <td>optimized</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  classifier   data_set       auc\n",
       "0        SGD   baseline  0.999074\n",
       "1        SGD  optimized  1.000000\n",
       "2         RF   baseline  0.984074\n",
       "3         RF  optimized  0.992963\n",
       "4         GB   baseline  0.991481\n",
       "5         GB  optimized  1.000000"
      ]
     },
     "execution_count": 964,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_results"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 965,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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OxZpCwsLIy8vjzNnzpQqUJw/fwWz+daXLWlns42MjMu3fZnadraj7Vd5WbPt7O3t9CVM/hCbDXk0aNAAd3d39uzZY2k7deoUaWlptGzZslj/GjVqcOjQoSJtP/zwA/b29gQHB5d5vSIiImI9mwUKJycn+vTpw8yZM9mxYwepqamMHTuWiIgIwsPDMZlMZGRkYDKZAIiOjmb79u0sWLCAkydP8tlnn/HKK6/Qp08fPDyUnkVERCoSm97YavTo0eTn5zN+/Hjy8/Np06YNsbGxAOzdu5fo6GgSExOJjIzk/vvv5/XXX2fBggUsWbIEX19fHnvsMQYPHmzLkkVERMQKNg0UDg4OxMTEEBMTU2xaZGRksSGOjh07FjuPQkRERCoePRxMREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcNsGigKCgqYPXs2UVFRNG3alFGjRpGZmVli//T0dEaNGkXTpk1p1aoVU6ZMIScnx4YVi4iIiDVsGigSEhLYuHEjcXFxJCUlkZ6ezsiRI2/Y12Qy8a9//YusrCxWr17NnDlz2L59O6+++qotSxYRERErONhqRSaTicTERCZNmkTr1q0BiI+Pp0OHDqSkpNCsWbMi/Tdv3kxGRgZr1qzB09MTgBEjRrBmzRpblSwiIiJWstkRioMHD5KdnU1ERISlLSgoiFq1apGcnFys/86dO7n33nstYQKgV69erF+/3ib1ioiIiPVsFijS09MBCAgIKNLu7+9vmfZbx48fp1atWsydO5f27dvToUMH4uLiyM3NtUm9IiIiYj2bDXnk5ORgb2+Po6NjkXYnJ6cbhoQrV66wfv167rvvPubNm8fZs2d58cUXuXDhAnFxcaVat4+Ph6Ha5fby86ta3iWIAdp+lZe2nZQlmwUKFxcXzGYz+fn5ODj8ulqTyYSrq2vxwhwc8PT0ZObMmVSpUoXGjRuTn5/PM888Q0xMDF5e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ERGEh4djMpm4ePEinp6euLi4FBvq8PDwuGG7iIiIlD+b3thq9OjRdO3alfHjxxMdHU1gYCDz5s0DYO/evURFRbF3715bliQiIiK3gc2OUAA4ODgQExNDTExMsWmRkZEcOnSoxHlfeumlsixNREREDNDDwURERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExTIFCREREDFOgEBEREcMUKERERMQwBQoRERExzKaBoqCggNmzZxMVFUXTpk0ZNWoUmZmZJfb/4IMP6NatG+Hh4TzwwAMsXryYgoICG1YsIiIi1rBpoEhISGDjxo3ExcWRlJREeno6I0eOvGHfzz//nHHjxvHoo4/y/vvv8+yzz7JkyRIWLVpky5JFRETECjYLFCaTicTERMaOHUvr1q0JDQ0lPj6elJQUUlJSivVfs2YNnTp14oknniA4OJjOnTvz5JNPsmHDBluVLCIiIlZysNWKDh48SHZ2NhEREZa2oKAgatWqRXJyMs2aNSvSf+jQobi5uRVps7e359KlSzapV0RERKxns0CRnp4OQEBAQJF2f39/y7TfatKkSZHXV65cYfXq1bRp06bsihQREZE/xGaBIicnB3t7exwdHYu0Ozk5kZube8t5hw0bRm5uLs8++2yp1+3j41HqeaTs+PlVLe8SxABtv8pL207Kks0ChYuLC2azmfz8fBwcfl2tyWTC1dW1xPkuXLjAsGHDOHLkCMuXL6dWrVqlXvf581cwmwtv2U87m21kZFy+7cvUtrMdbb/Ky5ptZ29vpy9h8ofY7KTMmjVrApCRkVGk/dy5c8WGQa47deoUjz/+OKdOnSIpKanYMIiIiIhUDDYLFA0aNMDd3Z09e/ZY2k6dOkVaWhotW7Ys1v/8+fNER0djNptZvXo1DRo0sFWpIiIiUko2G/JwcnKiT58+zJw5Ey8vL3x8fJg6dSoRERGEh4djMpm4ePEinp6eODk5MXXqVH7++WdWrFiBi4uL5ciGnZ0dvr6+tipb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W7duJS0tjT179vDll18yf/58GjduzPDhw1mzZg29e/dm48aNpa6/Xr16HD9+nDp16lh+Dh8+zJw5cwx/NiIi1tKQhwjXhie+/PJL+vTpw5gxYwgLCyMzM5Ply5fzf//3fyxfvrzIVR7VqlXDwcGBDz/8EE9PTzIyMpgzZw4mkwmTyYSDgwOpqakkJyczadIkvL292bx5M46OjoSGhnL27Fnmz59P1apVadeuHZmZmezevZvw8PBS1z506FAGDx7M3/72Nzp16sTx48eJjY3l/vvv18mXImIzChQiXLvvQ1JSEkuWLOH111/nzJkzVK1albCwMNauXcvdd99d5CqPgIAAXn75ZRISElixYgUBAQF06dKFgIAAy501Z8+ezcsvv8zgwYPJzs6mfv36zJ8/33IU4eWXX2bp0qXMmjULDw8POnbsyHPPPVfq2u+77z5mzpzJ4sWLee211/D29qZ79+6MGTPmtn0+IiK3ojtlioiIiGE6h0JEREQMU6AQERERwxQoRERExDAFChERETFMgUJEREQMU6AQERERwxQoRERExDAFChERETFMgUJEREQM+39DWxKbNs1suwAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "import seaborn as sns\n",
    "import matplotlib.pyplot as plt\n",
    "sns.set(style=\"darkgrid\")\n",
    "\n",
    "ax = sns.barplot(x=\"classifier\", y=\"auc\", hue=\"data_set\", data=df_results)\n",
    "ax.set_xlabel('Classifier',fontsize = 15)\n",
    "ax.set_ylabel('AUC', fontsize = 15)\n",
    "ax.tick_params(labelsize=15)\n",
    "# Put the legend out of the figure\n",
    "plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0., fontsize = 15)\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The best model for my prediction is Random forest. as the basline and optimized model give the similar result. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 966,
   "metadata": {},
   "outputs": [],
   "source": [
    "pickle.dump(rf_random.best_estimator_, open('best_classifier.pkl', 'wb'),protocol = 4)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Model Evaluation"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "WEEK 5: evaluate the performance of your best model on the training, validation and test sets. Make an ROC curve too."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 967,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Your code here\n",
    "import pandas as pd\n",
    "import numpy as np\n",
    "import matplotlib.pyplot as plt\n",
    "import pickle"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 968,
   "metadata": {},
   "outputs": [],
   "source": [
    "# load the model, columns, mean values, and scaler\n",
    "best_model = pickle.load(open('best_classifier.pkl','rb'))\n",
    "cols_input = pickle.load(open('cols_input.sav','rb'))\n",
    "df_mean_in = pd.read_csv('df_mean.csv', names =['col','mean_val'])\n",
    "scaler = pickle.load(open('scaler.sav', 'rb'))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 969,
   "metadata": {},
   "outputs": [],
   "source": [
    "# load the data\n",
    "df_train = pd.read_csv('df_train.csv')\n",
    "df_valid= pd.read_csv('df_valid.csv')\n",
    "df_test= pd.read_csv('df_test.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 970,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\sklearn\\utils\\validation.py:475: DataConversionWarning: Data with input dtype int64 was converted to float64 by StandardScaler.\n",
      "  warnings.warn(msg, DataConversionWarning)\n",
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\sklearn\\utils\\validation.py:475: DataConversionWarning: Data with input dtype int64 was converted to float64 by StandardScaler.\n",
      "  warnings.warn(msg, DataConversionWarning)\n",
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\sklearn\\utils\\validation.py:475: DataConversionWarning: Data with input dtype int64 was converted to float64 by StandardScaler.\n",
      "  warnings.warn(msg, DataConversionWarning)\n"
     ]
    }
   ],
   "source": [
    "# fill missing\n",
    "df_train = fill_my_missing(df_train, df_mean_in, cols_input)\n",
    "df_valid = fill_my_missing(df_valid, df_mean_in, cols_input)\n",
    "df_test = fill_my_missing(df_test, df_mean_in, cols_input)\n",
    "\n",
    "# create X and y matrices\n",
    "X_train = df_train[cols_input].values\n",
    "X_valid = df_valid[cols_input].values\n",
    "X_test = df_test[cols_input].values\n",
    "\n",
    "y_train = df_train['OUTPUT_LABEL'].values\n",
    "y_valid = df_valid['OUTPUT_LABEL'].values\n",
    "y_test = df_test['OUTPUT_LABEL'].values\n",
    "\n",
    "# transform our data matrices \n",
    "X_train_tf = scaler.transform(X_train)\n",
    "X_valid_tf = scaler.transform(X_valid)\n",
    "X_test_tf = scaler.transform(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 971,
   "metadata": {},
   "outputs": [],
   "source": [
    "y_train_preds = best_model.predict_proba(X_train_tf)[:,1]\n",
    "y_valid_preds = best_model.predict_proba(X_valid_tf)[:,1]\n",
    "y_test_preds = best_model.predict_proba(X_test_tf)[:,1]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 972,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Training:\n",
      "AUC:1.000\n",
      "accuracy:1.000\n",
      "recall:1.000\n",
      "precision:1.000\n",
      "specificity:1.000\n",
      "prevalence:0.500\n",
      " \n",
      "Validation:\n",
      "AUC:0.993\n",
      "accuracy:0.930\n",
      "recall:0.926\n",
      "precision:0.971\n",
      "specificity:0.940\n",
      "prevalence:0.684\n",
      " \n",
      "Test:\n",
      "AUC:0.994\n",
      "accuracy:0.956\n",
      "recall:0.948\n",
      "precision:0.991\n",
      "specificity:0.952\n",
      "prevalence:0.734\n",
      " \n"
     ]
    }
   ],
   "source": [
    "thresh = 0.5\n",
    "\n",
    "print('Training:')\n",
    "train_auc, train_accuracy, train_recall, train_precision, train_specificity = print_report(y_train,y_train_preds, thresh)\n",
    "print('Validation:')\n",
    "valid_auc, valid_accuracy, valid_recall, valid_precision, valid_specificity = print_report(y_valid,y_valid_preds, thresh)\n",
    "print('Test:')\n",
    "test_auc, test_accuracy, test_recall, test_precision, test_specificity = print_report(y_test,y_test_preds, thresh)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 973,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "from sklearn.metrics import roc_curve \n",
    "\n",
    "fpr_train, tpr_train, thresholds_train = roc_curve(y_train, y_train_preds)\n",
    "auc_train = roc_auc_score(y_train, y_train_preds)\n",
    "\n",
    "fpr_valid, tpr_valid, thresholds_valid = roc_curve(y_valid, y_valid_preds)\n",
    "auc_valid = roc_auc_score(y_valid, y_valid_preds)\n",
    "\n",
    "fpr_test, tpr_test, thresholds_test = roc_curve(y_test, y_test_preds)\n",
    "auc_test = roc_auc_score(y_test, y_test_preds)\n",
    "\n",
    "plt.plot(fpr_train, tpr_train, 'r-',label ='Train AUC:%.3f'%auc_train)\n",
    "plt.plot(fpr_valid, tpr_valid, 'b-',label ='Valid AUC:%.3f'%auc_valid)\n",
    "plt.plot(fpr_test, tpr_test, 'g-',label ='Test AUC:%.3f'%auc_test)\n",
    "plt.plot([0,1],[0,1],'k--')\n",
    "plt.xlabel('False Positive Rate')\n",
    "plt.ylabel('True Positive Rate')\n",
    "plt.legend()\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Conclusion"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Week 5: Briefly summarize your project and describe your performance as if you were talking to a CEO. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The project is to predict if the toddler shows Autism traits from pre-screening process, and should he/she be sent to further ASD diagnosis in clinics. The dataset had 1054 observations. It had both Numerical and Categorial features. The data had questions A1 to A10 asked to parents and there responses where given as 0 or 1. One hot encoding was done a feature for better prediction. Built a test,train and validation dataset. Check the performances of baseline model. Accordiing to AUC(Area under curve) the best model is Random Forest. To model is underfitted, so to improve it we can had more feature or regularize the model. Then hyper tuning was done to check optimize and baseline model. The best model for my prediction is Randome forest with Acurracy of 99.4% in test, 99.3% in validation, and 100% in train."
   ]
  }
 ],
 "metadata": {
  "anaconda-cloud": {},
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
   "version": "3.7.0"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}


