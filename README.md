# Project88

#Test API Endpoint
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



#Test GET Search Recipe by Ingredients 
print("Three Ingredient Recipe Search!")
ing_1 = input("What is your first ingredient: ")
ing_2 = input("What is your second ingredient: ")
ing_3 = input("What is your third ingredient: ")
response = requests.get("https://spoonacular-recipe-food-nutrition-v1.p.rapidapi.com/recipes/findByIngredients?number=5&ranking=1&ignorePantry=false&ingredients="+ing_1+"%2C"+ing_2+"%2C"+ing_3,
  headers={
    "X-RapidAPI-Host": "spoonacular-recipe-food-nutrition-v1.p.rapidapi.com",
    "X-RapidAPI-Key": "b343d4d527mshf7013a9b6055945p136a3bjsnff731be0566b"
  }
)

response.json()

result = json.loads(response)
