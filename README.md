# Developpement-de-bacteries-vivantes-dans-les-matieres-fecales-des-souris-
# Graphique présentant le développement des bactéries dans les matières fécales de 2 populations de souris auxquelles a été administré soit un traitement placebo soit un traitement antibactérien (ABX) avant et après le jour du lavage de ces traitements.
import matplotlib.pyplot as plt
import math

# create graph data (instanciate graph)
figure, axes = plt.subplots()

# set titles
axes.set_title('Bactérie vivante dans les matières fécales')
axes.set_ylabel('Bactérie vivante en g')
axes.set_xlabel('nbr de jours')

graph = "fecal"

# init data
for mouse in range(17,33):
    x  = []
    y  = []

    # fill data from file
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
            x.append(day)
            y.append(bacteria)        

    fIN.close()

    axes.plot(x,y)


figure.savefig('resultat fecal.png', dpi=300)
