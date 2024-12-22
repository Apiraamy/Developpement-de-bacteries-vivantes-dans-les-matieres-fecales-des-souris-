# Developpement-de-bacteries-vivantes-dans-les-matieres-fecales-des-souris-
# Graphique présentant le développement des bactéries dans les matières fécales de 2 populations de souris auxquelles a été administré soit un traitement placebo soit un traitement antibactérien (ABX) avant et après le jour du lavage de ces traitements.
import matplotlib.pyplot as plt
import math

# create graph data (instanciate graph)
figure, axes = plt.subplots()

# nommer les titres et les axes 
axes.set_title('Bactéries vivantes dans les matières fécales')
axes.set_ylabel('Bactéries vivantes en g')
axes.set_xlabel('Nombre de jours avant et après le jour de lavage des traitements')

graph = "fecal"

# initialiser les données
for mouse in range(17,33):
    x  = []
    y  = []

    # remplir les données issues du document fourni
    fIN = open('data_filtrer.csv', 'r')
    line = fIN.readline()

    while line != '':
        line = fIN.readline()
        if line == '':
            break 
        # split line
        valueList = line.split(':')
        # retrieve data
        sample_type = valueList[0]
        print(valueList)
        mouse_ID    = int(valueList[1].replace('ABX', ''))
        treatment   = valueList[2]    
        day         = valueList[3]
        bacteria    = math.log(float(valueList[4]))/math.log(10)

        # filter lines
        if mouse_ID == mouse and sample_type == graph :
            x.append(jour)
            y.append(bacteries)        

    fIN.close()

    axes.plot(x,y)


figure.savefig('resultat fecal.png', dpi=300)
