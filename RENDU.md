# Rendu — Atelier Kubernetes

> Complétez ce fichier au fil de l'atelier, puis faites un commit et un push (voir la section « Rendu » du README).

**Nom / Prénom :** LEDRU Victor
**Groupe :** RS2

---

## Exercice 1 — Cluster

1. Combien de nœuds affiche `kubectl get nodes` ? Quel est le rôle de chacun ?
   > il y a 3 noeud, le premier est le control plane et les 2 autres sont des workers
2. Que montre `docker ps` ? Qu'est-ce qu'un « nœud » dans k3d, concrètement ?
   > docker ps renvoie les 3 nodes et un load balancer, soit 4 conteneur. donc un noeud dans k3d est un docker/conteneur

## Exercice 2 — Premier déploiement

3. Quels objets Kubernetes ont été créés par `kubectl create deployment` ? (indice : `kubectl get all`)
   > il a créé 4 objet : le pod web, le deployment.apps et le replicatset.app et le service web
4. Vous avez supprimé le pod `web-...` : que s'est-il passé, et pourquoi ?
   > kubernetes a supprimé le pod puis quelque seconde après il en a créé un nouveau

## Exercice 3 — Modifier un conteneur en direct

5. Après suppression du pod, votre message « Bienvenue... » a-t-il survécu ? Pourquoi ?
   > non apres la suppresion du pod le message a disparu car on la modifie dans le pod lui même et non dans l'image nginx
6. Pourquoi le `port-forward` a-t-il cessé de fonctionner après la suppression du pod ?
   >  car le nouveau pod a un autre nom donc le tunnel perd sa cible

## Exercice 4 — Déclaratif

7. Quelle différence entre `kubectl create` et `kubectl apply` ?
   > l'option create n'est faisable qu'une fois, une fois le pod creer il faut apply pour le modifier a volonté.
8. À quoi sert le `selector` d'un Service ? Que se passe-t-il s'il ne correspond à aucun pod ?
   > il indique quels pods reçoivent le trafic. s'il ne correspond a aucun pod le service est quand même crée mais les Endpoint sont vides

## Exercice 5 — Scaling & mises à jour

9. Sur quels nœuds se trouvent vos 3 réplicas ? Collez la sortie de `kubectl get pods -l app=site -o wide`. chaque replica tourne sur un noeud différent, agent 0, 1 et lab-server NAME                    READY   STATUS    RESTARTS   AGE   IP           NODE               NOMINATED NODE   READINESS GATES
site-5cc664db9c-75cq7   1/1     Running   0          61s   10.42.1.6    k3d-lab-server-0   <none>           <none>
site-5cc664db9c-9glh5   1/1     Running   0          70s   10.42.0.18   k3d-lab-agent-0    <none>           <none>
site-5cc664db9c-mp9ht   1/1     Running   0          76s   10.42.2.12   k3d-lab-agent-1    <none>           <none>
   ``` 

   ```
10. Avec l'image `nginx:9.99`, quel statut avait le pod ? Quelle commande vous a donné la cause ?
    > le pod etait en errimagepull puis ImagePullBackOff, donc il narrive pas a recuperer l'image. la commande est kubectl describe pod site-fc576997-j925p (le nom du pod)
11. Pendant la panne, le site restait-il accessible ? Pourquoi ?
    > oui car la mise a jour est une rolling update donc ne coupe pas les anciens pods tant que les nouveaux ne sont pas en ligne.

## Exercice 6 — Portainer & Mario

12. URL publique de votre Mario :
    > https://silver-invention-jqxpxv9xvpq3prpg-8585.app.github.dev/
13. Retrouvez le Deployment `mario` en ligne de commande. Portainer et `kubectl` parlent-ils au même composant ? Lequel ?
    > oui ils parlent tout les deux a l'api du server kubernetes

## Bonus (facultatif)

14. Bonus réalisés et remarques :
    >

---

**Score obtenu avec `./scripts/check.sh` :** ... / ...
