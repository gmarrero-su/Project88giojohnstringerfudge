# Project88
#Test API Endpoint for Recipe Generator
#Import the neccesary libraries and programs
import requests
import json
from IPython.display import display


response = requests.get("https://spoonacular-recipe-food-nutrition-v1.p.rapidapi.com/recipes/quickAnswer?q=How+much+vitamin+c+is+in+2+apples%3F",
  headers={
    "X-RapidAPI-Host": "spoonacular-recipe-food-nutrition-v1.p.rapidapi.com",
    "X-RapidAPI-Key": "b343d4d527mshf7013a9b6055945p136a3bjsnff731be0566b"
  }
)

response.json()

count = 0

#Instructs the user to give 3 ingredients to generate a recipe

print("Please give me 3 ingredients that you have to make a proper recipe dish!")

ing_1 = input("What is your first ingredient: ")
ing_2 = input("What is your second ingredient: ")
ing_3 = input("What is your third ingredient: ")

#To add blank space for stylization

print('')

#Our API to get a recipe using ingredient search functions

response = requests.get("https://spoonacular-recipe-food-nutrition-v1.p.rapidapi.com/recipes/findByIngredients?number=5&ranking=1&ignorePantry=false&ingredients="+ing_1+"%2C"+ing_2+"%2C"+ing_3,
  headers={
    "X-RapidAPI-Host": "spoonacular-recipe-food-nutrition-v1.p.rapidapi.com",
    "X-RapidAPI-Key": "b343d4d527mshf7013a9b6055945p136a3bjsnff731be0566b"
  }
)

data = response.json()


#An error message when non-ingredients are detected

try: missed_ing_count = data[0]['missedIngredientCount']
except IndexError:
    print("These are not ingredients! Please try again")
    
#To get the ID number of the recipe, used to identify recipe and get hyperlink
id_number = str(data[0]['id'])
    

#Our output of the recipe using the API

print("Your recipe is:")
print(data[0]['title'])
flick = (data[0]['image'])
print(flick)
#image = flick.open('File.jpg')
#image.show()

#To add blank space for stylization
print('')

#An output of ingredients that are still needed to make the meal

missed_ings = data[0]['missedIngredients']
print("Your missing ingredients are:")

#While statement and count to allow multiple ingredients to be displayed

while(missed_ing_count != count):
    print(missed_ings[0 + count]['name'])
    count = count + 1

#To add blank space for stylization
print('')
    
#The API to generate the URL hyperlink of the recipe using the specific ID code in the system
    
response = requests.get("https://spoonacular-recipe-food-nutrition-v1.p.rapidapi.com/recipes/"+id_number+"/information",
  headers={
    "X-RapidAPI-Host": "spoonacular-recipe-food-nutrition-v1.p.rapidapi.com",
    "X-RapidAPI-Key": "b343d4d527mshf7013a9b6055945p136a3bjsnff731be0566b"
  }
)


url_data = response.json()

print("Here is the recipe! Bon appetit!")

#This will give a functional hyperlink for instructions directly as an output.

print(url_data['sourceUrl'])
