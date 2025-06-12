# Introduction :

Avant de commencer, il faut se rendre dand le dossier dans lequel se situe le fichier data.csv qui contient toutes les données qui permettront d'effectuer nos analyses.

On entre la commande 
```
-->csv = csvRead('data.csv',',');                    
```
On met dans la variable csv tout le contenu quantitatif du fichier de data
```                                
-->data = csvRead('data.csv', ",", [], "string") 
```
Avec cette ligne là, on y met les valeurs quantitatives telles que le genre le niveau scolaire, etc.


# exercice 1: 

Avant de pouvoir donner les données sous forme de tableau, nous les calculons d'abord. Les valeurs numériques en question sont l'age, la moyenne d'utilisation quotidienne, le nombre d'heures de sommeil et enfin une note sur 10 indiquant la santé mentale de chacun des étudiants.
Pour cela, on associe à une variable chaque colonne : 


```
-->age = csv(:,2);                         
-->temps_decran = csv(:,6);
-->sommeil = csv(:,9);
-->sante_mentale = csv(:,10);
```

```
-->moyenne_age = mean(age);                On déclare la variable moyenne_age qui va contenir la moyenne de l'age grace à la fonction mean() 
                                           qui prend en paramètre la série statistique dont je veux la moyenne. On effectue la même commande mais avec temps_decran, sommeil et sante_mentale.



-->disp(moyenne_age)                       On peut afficher le contenu de chaque nouvelle variable grâce à la fonction disp.
20.659574
```


# exercice 2 

## 1)

```
age = csv(:,2);

--> ages = csv(:,2);                    
--> tab = tabul(ages);                   
--> disp(tab);                          

   24.   26. 
   23.   34. 
   22.   147.
   21.   156.
   20.   165.
   19.   163.
   18.   14. 

--> bar(tab(:,1), tab(:,2));
--> xtitle("Effectif des âges", "Âge", "Effectif");
```


Ici, nous avons besoin de lire les données qualitatives

```
-->data = csvRead('data.csv', ",", [], "string")

 --> genre = data(:,3)         
-->tab = tabul(genre);        
--> disp(tab2);                

  (1) = ["Male";"Female"]
  (2) = [352;353]

-->pie(tab(2), tab(1));

--> xtitle("Répartition des genres");
```



## 2)
```
-->pays = data(:,5);
-->premierspays = ["Bangladesh", "India", "USA", "UK", "Canada", "Australia", "Germany", "Brazil", "Japan", "South Korea"];
-->n = size(premierspays, 2);

--> effectifs = zeros(1, n);

--> for i = 1:n
  >     effectifs(i) = sum(pays == premierspays(i));
  > end

--> disp([premierspays' string(effectifs')], "Pays et effectifs");

  "Bangladesh"   "20"
  "India"        "53"
  "USA"          "40"
  "UK"           "22"
  "Canada"       "34"
  "Australia"    "14"
  "Germany"      "14"
  "Brazil"       "8" 
  "Japan"        "21"
  "South Korea"  "13"

  "Pays et effectifs"
-->bar(effectifs);
-->xtitle("Nombre d etudiants par pays (Top 10)");     
```

## 3)
```
-->niveaux = data(:,4);
--> categories = ["High School", "Undergraduate", "Graduate"];
-->effectifs = zeros(1, size(categories, 2));
--> for i = 1:size(categories, 2)
  >     effectifs(i) = sum(niveaux == categories(i));
  > end
--> disp([categories' string(effectifs')], "Niveau scolaire et effectifs");

  "High School"    "27" 
  "Undergraduate"  "353"
  "Graduate"       "325"

  "Niveau scolaire et effectifs"

-->clf();
--> bar(effectifs);
--> xtitle("Répartition des étudiants par niveau scolaire");
```

## 4) 
```
-->plateformes_cibles = ["TikTok", "Instagram", "Facebook", "Twitter", "YouTube", "LinkedIn", "Snapchat"];
--> temps_txt = data(:,6);
--> plateformes_raw = data(:,7); 
--> plateformes = stripblanks(plateformes_raw);
--> n = size(temps_txt, 1);
--> temps = zeros(n, 1);
--> for i = 1:n
  >     temps(i) = evstr(temps_txt(i)); // convertit "4.5" → 4.5
  > end
--> nb = size(plateformes_cibles, 2);
--> moyennes = zeros(1, nb);
--> for i = 1:nb
  >     indices = find(plateformes == plateformes_cibles(i));
  >     if size(indices, "*") > 0 then
  >         moyennes(i) = mean(temps(indices));
  >     else
  >         moyennes(i) = 0; 
  >     end
  > end
--> resultats = [plateformes_cibles' string(moyennes')];
--> disp(resultats, "Temps moyen ciblé par réseau");

  "TikTok"     "5.3461039"
  "Instagram"  "4.8722892"
  "Facebook"   "4.5073171"
  "Twitter"    "4.87"     
  "YouTube"    "4.08"     
  "LinkedIn"   "2.5190476"
  "Snapchat"   "5.0923077"

  "Temps moyen ciblé par réseau"
--> scf(0); clf();
--> bar(moyennes);
--> 
--> xtitle("Temps moyen d’utilisation par réseau social (h/jour)");
```


# exercice 3:
## 1)
VERSION AVEC BOXPLOT: POUR 16-20
```

data = csvRead("data.csv", ",");


age = data(:, 2);
temps = data(:, 6);


id_16_20 = find(age >= 16 & age <= 20);
temps_16_20 = temps(id_16_20);


mean(temps_16_20)         // moyenne
min(temps_16_20)          // min
max(temps_16_20)          // max
median(temps_16_20)       // médiane
quart(temps_16_20)        // quartiles (Q1 et Q3)
iqr(temps_16_20)          // intervalle interquartile
stdev(temps_16_20)        // écart-type


tab = tabul(temps_16_20);
[occurences, indices] = gsort(tab(:,2));
valeurs = tab(:,1);
mode_16_20 = valeurs(indices(1))      // mode


clf();
boxplot(temps_16_20, "orientation", "horizontal");
xlabel('Temps d''utilisation (heures)');
title('Boîte à moustache - Groupe 16–20 ans');

```
AVEC BOXPLOT POUR 21-25
```

id_21_25 = find(age >= 21 & age <= 25);
temps_21_25 = temps(id_21_25);


mean(temps_21_25)
min(temps_21_25)
max(temps_21_25)
median(temps_21_25)
quart(temps_21_25)
iqr(temps_21_25)
stdev(temps_21_25)


tab = tabul(temps_21_25);
[occurences, indices] = gsort(tab(:,2));
valeurs = tab(:,1);
mode_21_25 = valeurs(indices(1))      


clf();
boxplot(temps_21_25, "orientation", "horizontal");
xlabel('Temps d''utilisation (heures)');
title('Boîte à moustache - Groupe 21–25 ans');
```
VERSION SANS BOXPLOT (cf une erreur) pour 16-20
```

data = csvRead("data.csv", ",");
age = data(:, 2);
temps = data(:, 6);


id_16_20 = find(age >= 16 & age <= 20);
temps_16_20 = temps(id_16_20);


quartiles = quart(temps_16_20); 
Q1 = quartiles(1);
Q2 = quartiles(2);
Q3 = quartiles(3);
IQR = Q3 - Q1;
Min = min(temps_16_20);
Max = max(temps_16_20);

Binf = Q1 - 1.5 * IQR;
Bsup = Q3 + 1.5 * IQR;
valeurs_valides = temps_16_20(temps_16_20 >= Binf & temps_16_20 <= Bsup);
borne_min = min(valeurs_valides);
borne_max = max(valeurs_valides);


clf();
x = 1;        
h = 0.1;      

plot2d([], []); 


xpoly([Q1 Q3 Q3 Q1 Q1], [x-h x-h x+h x+h x-h], "lines");


xpoly([Q2 Q2], [x-h x+h], "lines");


xpoly([borne_min Q1], [x x], "lines");
xpoly([Q3 borne_max], [x x], "lines");


outliers = temps_16_20(temps_16_20 < Binf | temps_16_20 > Bsup);
for i = 1:length(outliers)
    plot2d(outliers(i), x, style=5); // style 5 = point noir
end


xtitle('Boîte à moustaches - Temps d''utilisation (16–20 ans)');
xlabel('Temps (heures)');
ylabel('Groupe');


a = gca();
a.y_ticks.locations = [1];
a.y_ticks.labels = ["16-20 ans"]';
a.data_bounds = [Min - 1, x - 0.5; Max + 1, x + 0.5];

show_window(); 


```

VERSION SANS BOXPLOT 21-25
```

data = csvRead("data.csv", ",");
age = data(:, 2);
temps = data(:, 6);

id_21_25 = find(age >= 21 & age <= 25);
temps_21_25 = temps(id_21_25);


quartiles = quart(temps_21_25);
Q1 = quartiles(1);
Q2 = quartiles(2);
Q3 = quartiles(3);
IQR = Q3 - Q1;
Min = min(temps_21_25);
Max = max(temps_21_25);


Binf = Q1 - 1.5 * IQR;
Bsup = Q3 + 1.5 * IQR;
valeurs_valides = temps_21_25(temps_21_25 >= Binf & temps_21_25 <= Bsup);
borne_min = min(valeurs_valides);
borne_max = max(valeurs_valides);


clf();
x = 1;         
h = 0.1;       

plot2d([], []); 


xpoly([Q1 Q3 Q3 Q1 Q1], [x-h x-h x+h x+h x-h], "lines");


xpoly([Q2 Q2], [x-h x+h], "lines");


xpoly([borne_min Q1], [x x], "lines");
xpoly([Q3 borne_max], [x x], "lines");

outliers = temps_21_25(temps_21_25 < Binf | temps_21_25 > Bsup);
for i = 1:length(outliers)
    plot2d(outliers(i), x, style=5); 
end


xtitle('Boîte à moustaches - Temps d''utilisation (21–25 ans)');
xlabel('Temps (heures)');
ylabel('Groupe');

a = gca();
a.y_ticks.locations = [1];
a.y_ticks.labels = ["21-25 ans"]';
a.data_bounds = [Min - 1, x - 0.5; Max + 1, x + 0.5];

show_window(); 
```
```
##2)
```



# exercice 4:

```
temps = data(:, 6);
performance = data(:, 10);

groupes = ["0-2h", "2-4h", "4-6h", "6-12h"];
moyennes = zeros(1, 4);

moyennes(1) = mean(performance(temps >= 0 & temps < 2));
moyennes(2) = mean(performance(temps >= 2 & temps < 4));
moyennes(3) = mean(performance(temps >= 4 & temps < 6));
moyennes(4) = mean(performance(temps >= 6 & temps <= 12));

clf();
bar(moyennes);
xtitle('Impact de la durée d''utilisation des réseaux sur la performance académique');
ylabel('Performance académique moyenne');

axes = gca();
axes.x_ticks.locations = 1:4;
axes.x_ticks.labels = groupes(:); // vecteur colonne

show_window();
```


# exercice 5: 

```

data = csvRead("data.csv", ",");
sommeil = data(:, 9);         
addiction = data(:, 13);     

groupes = ["<5h", "5-7h", "7-9h", ">9h"];
moyennes = zeros(1, 4);

moyennes(1) = mean(addiction(sommeil < 5));
moyennes(2) = mean(addiction(sommeil >= 5 & sommeil < 7));
moyennes(3) = mean(addiction(sommeil >= 7 & sommeil < 9));
moyennes(4) = mean(addiction(sommeil >= 9));

clf();
bar(moyennes);
xtitle('Score d'addiction en fonction de la durée de sommeil');
ylabel('Score moyen d''addiction');

axes = gca();
axes.x_ticks.locations = 1:4;
axes.x_ticks.labels = groupes(:);

show_window();
```



# exercice 6:

1)**A revoir**

```
groupes = ["<2h", "2-4h", "4-6h", "6h+"];

moy_h = [8.00, 7.81, 6.91, 5.83];
moy_f = [%nan, 8.32, 6.79, 5.57]; 

for i = 1:size(moy_f, 2)
    if isnan(moy_f(i)) then
        moy_f(i) = 0.01; // Valeur minimale visible
    end
end

clf();
bar([moy_h' moy_f']);

xlabel("Durée d utilisation des réseaux");
ylabel("Heures de sommeil");
xtitle("Sommeil moyen selon le temps passé sur les réseaux");

axes = gca();
n = size(groupes, 2);
 
axes.x_ticks.labels = groupes(:);

legend(["Hommes", "Femmes"], "upper_right");

indiquer qu’il n’y avait aucune donnée
xstring(1 - 0.25, 0.2, "aucune donnée");

```

2) Il existe clairement un lien entre les deux, il est évident en analysant l'histogramme que plus nous consacrons du temps aux réseaux sociaux, moins nous dormons.

3)Il existe bien évidemment une corélation entre l'addiction aux réseaux sociaux et les conflits sur les réseaux sociaux : 
  
```
data = csvRead("data.csv", ",");

addiction = data(:, 13); 
conflicts = data(:, 12); 

// Scores possibles (on suppose 0 à 5)
scores = unique(addiction);
nb = size(scores, "*");

moyenne_conflits = zeros(1, nb);

for i = 1:nb
    indices = addiction == scores(i);
    moyenne_conflits(i) = mean(conflicts(indices));
end

clf();
plot(scores, moyenne_conflits, "-o");

xtitle("Lien entre score d addiction et conflits sur les réseaux");
xlabel("Score d addiction");
ylabel("Nombre moyen de conflits");

// Grille
xgrid(1);
```


# exercice 7 

Parlons de la santé mentale et de l'addiction, comme pour les drogues, plus on est addict, plus ça va mal : 
```
data = csvRead("data.csv", ",", [], "string");

ment_raw = stripblanks(strsubst(data(:,10), """", ""));
add_raw  = stripblanks(strsubst(data(:,13), """", ""));

ment_score = strtod(ment_raw);
add_score  = strtod(add_raw);

clf();
plot(add_score, ment_score, 'o');
xtitle("Mental Health Score vs Addiction Score", "Addiction Score", "Mental Health Score");

```

Avec un jitter :
```
data = csvRead("data.csv", ",", [], "string");

add_raw  = stripblanks(strsubst(data(:,13), """", ""));
ment_raw = stripblanks(strsubst(data(:,10), """", ""));

add_score  = strtod(add_raw);
ment_score = strtod(ment_raw);

ok = find(~(isnan(add_score) | isnan(ment_score)));
AS = add_score(ok);   // 705×1
MS = ment_score(ok);  // 705×1

n   = size(AS, "r");          // =705
j_x = (rand(n, 1) - 0.5) * 0.2;  
j_y = (rand(n, 1) - 0.5) * 0.2;  

clf();
plot(AS + j_x, MS + j_y, 'o');
xtitle("Addiction vs Mental Health (jitter)", "Addiction Score", "Mental Health Score");
```
