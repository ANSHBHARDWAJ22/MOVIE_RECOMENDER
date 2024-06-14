# MOVIE_RECOMENDER
I have developed a basic movie recommender system designed to suggest five movies similar to a user-provided input. This system leverages key algorithms and data processing techniques to analyze movie characteristics and user preferences, delivering tailored recommendations efficiently.

THIS IS THE STREAMLIT CODE ->

import pickle

import pandas as pd
import streamlit as st


def recommend(movie):
    index = movies[movies['title'] == movie].index[0]
    distances = sorted(list(enumerate(similarity[index])), reverse=True, key=lambda x: x[1])

    recommend_movie=[]
    for i in distances[1:6]:
        movieid=i[0]
        # fetch poster from api

        recommend_movie.append(movies.iloc[i[0]].title)
    return  recommend_movie


st.title("movie recomender")


# for background  ->

primaryColor = "#f63366"
backgroundColor = "#FFFFFF"
secondaryBackgroundColor = "#f0f2f6"
textColor = "#262730"
font = "sans serif"

movies_dict=pickle.load(open('movie_dict.pkl','rb'))
movies=pd.DataFrame(movies_dict)

similarity=pickle.load(open('similarity.pkl','rb'))

option = st.selectbox(
    "enter movie name ",
    (
movies['title'].values))




if st.button("recommend"):
    recomendations=recommend(option)
    for i in recomendations:
        st.write(i)

