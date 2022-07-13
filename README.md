# exercice-git-merge-defi

## 1. Sur une branche master sans commits, créez un fichier index.html (cf. contenu en fin d'exercice)
$ vi index.html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
  </head>
  <body>
    <h1>Liste des fruits :</h1>
    <ul>
      <li>Pome</li>
      <li>Carote</li>
      <li>Salade</li>
      <li>Poire</li>
      <li>Tommate</li>
      <li>Cerisse</li>
    </ul>
  </body>
</html>

## 2. Ajoutez le fichier et créez un commit nommé Add fruit list
$ git add index.html              (1)
$ git commit -m "Add fruit list"  (2)

## 3. Poussez la branche master sur votre dépôt distant en définissant l'upstream après l'avoir créé sur GitHub
$ git remote add origin git@github.com:(organisme)/(repository)
$ git push -u origin master

## 4. Créez une branche fix-typos depuis ce commit, placez-vous dessus, puis modifiez le texte du fichier pour corriger les fautes de frappe
$ git checkout -b fix-typos
$ sed -i _ 's/Pome/Pomme/g; s/Carote/Carotte/g; s/Tommate/Tomate/g; s/Cerisse/Cerise/g' index.html
cette commande modifie le fichier index.html et concerve une copie avant modification dans index.html_
l'option i sans argument de la command sed provoque une erreur sous osx

## 5. Créez un commit nommé Fix typos in fruit list, puis poussez-le sur GitHub
$ git add index.html                        (1)
$ git commit -m "Fix typos in fruit list"   (2)
$ git push -u origin fix-typos              (3)

## 6. Créez une nouvelle branche remove-vegetables depuis master, puis modifiez le fichier pour corriger la liste en supprimant les légumes
$ git checkout -b remove-vegetables master
$ sed -i_ '/Carote/d; /Salade/d; /Tomate/d' index.html

## 7. Créez un commit nommé Remove vegetables from fruit list, puis poussez-le sur GitHub
$ git add index.html                                (1)
$ git commit -m "Remove vegetables from fruit list" (2)
$ git push -u origin remove-vegetables              (3)

## 8. Fusionnez la branche fix-typos dans la branche master et pousser
$ git checkout master (1)
$ git merge fix-typos (2)
$ git push            (3)

## 9. Fusionnez la branche remove-vegetables dans la branche master (vous devriez avoir des conflits)
$ git merge remove-vegetables

## 10. Résolvez les conflits en gardant les corrections des deux branches et terminez la fusion, puis poussez master de nouveau
   <body>
     <h1>Liste des fruits :</h1>
     <ul>
 -   <<<<<<< HEAD
       <li>Pomme</li>
 -     <li>Carotte</li>
 -     <li>Salade</li>
 -   =======
 -     <li>Pome</li>
       <li>Poire</li>
       <li>Tomate</li>
       <li>Cerise</li>
 -   >>>>>>> remove-vegetables
  
$ git commit     (2)
$ git push       (3)
  
## 11. Supprimez les branches fix-typos et remove-vegetables sur le dépôt distant et en local
$ git branch -d fix-typos && git branch -d remove-vegetables
$ git push origin -d fix-typos && git push origin -d remove-vegetables
