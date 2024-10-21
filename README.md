cook_book = {}
def reading_of_catalog():
    with open('recipes.txt', 'rt') as file:
        
          
        for line in file:
            dish_name = line.strip()
            cook_book[dish_name] = []
            for j in range(int(file.readline())):
                consist = file.readline().split(' | ')
                cook_book[dish_name].append({'ingredient_name': consist[0],
                                             'quantity': int(consist[1]),
                                              'measure': consist[2].strip()})
            file.readline()
    return cook_book
  
print(reading_of_catalog())

def list_of_stores_with_ingredients(dishes, person_count, cook_book):
    result = {}
    for dish in dishes:
        if dish in cook_book:
            for consist in cook_book[dish]:
                if consist['ingredient_name'] in result:
                    result[consist['ingredient_name']]['quantity'] += consist['quantity'] * person_count
                else:
                    result[consist['ingredient_name']] = {'measure': consist['measure'],
                                                       'quantity': (consist['quantity'] * person_count)}
        else:
            print(f'Блюда "{dish}" нет в книге рецептов')
    return result


person_count = 3
dishes = ['Омлет', 'Утка по-пекински', 'Запеченный картофель']

print(reading_of_catalog())
print()
print(list_of_stores_with_ingredients(dishes, person_count, cook_book))