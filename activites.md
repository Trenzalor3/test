---
title: "Activités"
order: 1
in_menu: true
---
>Il n'y a pas d'activités car ceci est un test.


Gluk 


| Texte a gauche | Texte au milieu | Texte a droite|
|:------------------|:------------------|:----------------|
| Ce texte          | ce texte           | Ce texte        |
| est aligné        | est                  | est aligné      |
| à gauche         | centré             | à droite         | 
| Ce texte         | ce texte        | Ce texte        |
| est aligné       | est             | est aligné      |
| à gauche         | centré          | à droite        |


```
from tkinter import *
from tkinter import ttk
from random import *
from tkinter.messagebox import *
from tkinter.simpledialog import *
import sys
import copy
## Fin d'importation des bibliothèques

## Classes
class Joueurs :
    ''' Définition d'un joueur '''
    def __init__ (self, nom, couleur, tour, manches = 0) :
        self.nom = nom
        self.couleur = couleur
        self.manches = manches
        self.tour = tour

    def incremente_manche (self, nbre) :
        self.manches += nbre

    def initialisation_manches (self) :
        self.manches = 0

    def change_couleur (self) :
        if self.couleur == "BLEU" :
            self.couleur = "VERT"
            self.tour = 0
        elif self.couleur == "VERT" :
            self.couleur = "BLEU"
            self.tour = 1    
## Fin classes

# Fonctions et procédures
def quitter_jeu () :
    ''' Fonction pour quitter le jeu '''
    reponse = messagebox.askyesno ("Terminer le jeu","Voulez-vous réellement quitter ? \n Cliquer sur « Oui » pour finir")
    if reponse :
        fen.destroy()

def cross_closing_windows():
    ''' Empêche fermeture de la fenêtre via la croix de fermeture '''
    return

def limitNom (*args) :
    ''' Procédure pour limiter nom des joueurs à 10 lettres '''
    nom1 = nomValue1.get ()
    if len(nom1) > 10 :
        nomValue1.set (nom1 [:10])
    nom2 = nomValue2.get ()
    if len(nom2) > 10 :
        nomValue2.set (nom2 [:10])

def menu_aide () :
    ''' Procédure de passage de la feuille 'Menu' à la feuille 'Aide' '''
    frame_menu.grid_remove ()
    frame_aide.grid ()

def aide_menu () :
    ''' Procédure de passage de la feuille 'Aide' à la feuille 'Menu' '''
    frame_aide.grid_remove ()
    frame_menu.grid ()

def aide_exemple () :
    ''' Procédure de passage de la feuille 'Aide' à la feuille 'Exemple' '''
    frame_exemple.grid ()
    frame_aide.grid_remove ()

def exemple_aide () :
    ''' Procédure de passage de la feuille 'Exemple' à la feuille 'Aide' '''
    frame_aide.grid ()
    frame_exemple.grid_remove ()

def menu_AP () :
    ''' Procédure de passage de la feuille 'Menu' à la feuille 'À Propos' '''
    frame_menu.grid_remove ()
    frame_ap.grid ()

def ap_menu () :
    ''' Procédure de passage de la feuille 'À Propos' à la feuille 'Menu' '''
    frame_ap.grid_remove ()
    frame_menu.grid ()

def retour_menu () :
    ''' Procédure de retour à la feuille 'Menu' après partie gagnée '''
    frame_jeu.grid_remove ()
    frame_menu.grid ()

def choix_joueur1 (event = None) :
    ''' Choix de la pièce à joueur pour le premier joueur '''
    global tailleJoueur1, nombreJoueur1G, nombreJoueur1M, nombreJoueur1P, liste_joueurs
    if canvas_joueur1_selection ["state"] == NORMAL : # Changement que si canvas actif
        if tailleJoueur1 == "G" : # Si grande taille activée
            if nombreJoueur1M > 0 : # Si il reste au moins une pièce moyenne à jouer
                tailleJoueur1 = "M" # On la sélectionne et on l'affiche dans le canvas après vidage de celui-ci
                canvas_joueur1_selection.delete (ALL)
                if liste_joueurs [0].couleur == "VERT" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgMCV, anchor = "nw")
                elif liste_joueurs [0].couleur == "BLEU" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgMCB, anchor = "nw")
            elif nombreJoueur1P > 0 : # Si pas de pièce moyenne et si il reste au moins une petite pièce à jouer
                tailleJoueur1 = "P" # On la sélectionne et on l'affiche dans le canvas après vidage de celui-ci
                canvas_joueur1_selection.delete (ALL)
                if liste_joueurs [0].couleur == "VERT" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgPCV, anchor = "nw")
                elif liste_joueurs [0].couleur == "BLEU" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgPCB, anchor = "nw")
        elif tailleJoueur1 == "M" : # Si taille moyenne activée, même vérifications qu'avec grande pièce et changement si possible
            if nombreJoueur1P > 0 :
                tailleJoueur1 = "P"
                canvas_joueur1_selection.delete (ALL)
                if liste_joueurs [0].couleur == "VERT" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgPCV, anchor = "nw")
                elif liste_joueurs [0].couleur == "BLEU" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgPCB, anchor = "nw")
            elif nombreJoueur1G > 0 :
                tailleJoueur1 = "G"
                canvas_joueur1_selection.delete (ALL)
                if liste_joueurs [0].couleur == "VERT" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgGCV, anchor = "nw")
                elif liste_joueurs [0].couleur == "BLEU" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgGCB, anchor = "nw")
        elif tailleJoueur1 == "P" : # Si petite taille activée, même vérifications qu'avec grande pièce et changement si possible
            if nombreJoueur1G > 0 :
                tailleJoueur1 = "G"
                canvas_joueur1_selection.delete (ALL)
                if liste_joueurs [0].couleur == "VERT" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgGCV, anchor = "nw")
                elif liste_joueurs [0].couleur == "BLEU" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgGCB, anchor = "nw")
            elif nombreJoueur1M > 0 :
                tailleJoueur1 = "M"
                canvas_joueur1_selection.delete (ALL)
                if liste_joueurs [0].couleur == "VERT" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgMCV, anchor = "nw")
                elif liste_joueurs [0].couleur == "BLEU" :
                    canvas_joueur1_selection.create_image (0, 0, image = imgMCB, anchor = "nw")

def choix_joueur2 (event = None) :
    ''' Choix de la pièce à joueur pour le second joueur '''
    global tailleJoueur2, nombreJoueur2G, nombreJoueur2M, nombreJoueur2P, liste_joueurs
    if canvas_joueur2_selection ["state"] == NORMAL : # Même principe que pour premier joueur
        if tailleJoueur2 == "G" :
            if nombreJoueur2M > 0 :
                tailleJoueur2 = "M"
                canvas_joueur2_selection.delete (ALL)
                if liste_joueurs [1].couleur == "VERT" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgMCV, anchor = "nw")
                elif liste_joueurs [1].couleur == "BLEU" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgMCB, anchor = "nw")
            elif nombreJoueur2P > 0 :
                tailleJoueur2 = "P"
                canvas_joueur2_selection.delete (ALL)
                if liste_joueurs [1].couleur == "VERT" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgPCV, anchor = "nw")
                elif liste_joueurs [1].couleur == "BLEU" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgPCB, anchor = "nw")
        elif tailleJoueur2 == "M" :
            if nombreJoueur2P > 0 :
                tailleJoueur2 = "P"
                canvas_joueur2_selection.delete (ALL)
                if liste_joueurs [1].couleur == "VERT" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgPCV, anchor = "nw")
                elif liste_joueurs [1].couleur == "BLEU" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgPCB, anchor = "nw")
            elif nombreJoueur2G > 0 :
                tailleJoueur2 = "G"
                canvas_joueur2_selection.delete (ALL)
                if liste_joueurs [1].couleur == "VERT" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgGCV, anchor = "nw")
                elif liste_joueurs [1].couleur == "BLEU" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgGCB, anchor = "nw")
        elif tailleJoueur2 == "P" :
            if nombreJoueur2G > 0 :
                tailleJoueur2 = "G"
                canvas_joueur2_selection.delete (ALL)
                if liste_joueurs [1].couleur == "VERT" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgGCV, anchor = "nw")
                elif liste_joueurs [1].couleur == "BLEU" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgGCB, anchor = "nw")
            elif nombreJoueur2M > 0 :
                tailleJoueur2 = "M"
                canvas_joueur2_selection.delete (ALL)
                if liste_joueurs [1].couleur == "VERT" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgMCV, anchor = "nw")
                elif liste_joueurs [1].couleur == "BLEU" :
                    canvas_joueur2_selection.create_image (0, 0, image = imgMCB, anchor = "nw")

def changement_tour () :
    ''' Procédure de changement de tour (manche terminée mais partie non gagnée) '''
    global liste_joueurs # On change de tour, on rend actif ou inactif chaque canvas de choix, et on met à jour l'information de qui joue
    if liste_joueurs [0].tour == 1 and liste_joueurs [1].tour == 0 :
        liste_joueurs [0].tour = 0
        liste_joueurs [1].tour = 1
        canvas_joueur1_selection.configure (state = DISABLED)
        canvas_joueur2_selection.configure (state = NORMAL)
        label_jeu_info.configure (text = "\nAU TOUR DE " + liste_joueurs [1].nom + " DE JOUER !\n")
    elif liste_joueurs [0].tour == 0 and liste_joueurs [1].tour == 1 :
        liste_joueurs [0].tour = 1
        liste_joueurs [1].tour = 0
        canvas_joueur1_selection.configure (state = NORMAL)
        canvas_joueur2_selection.configure (state = DISABLED)
        label_jeu_info.configure (text = "\nAU TOUR DE " + liste_joueurs [0].nom + " DE JOUER !\n")

def placement (event = None) :
    ''' Procédure de placement de la pièce choisie sur le plateau de jeu '''
    global tableau_jeu, partie_en_cours, liste_joueurs, tailleJoueur1, tailleJoueur2, tableau_bleu, tableau_vert, nombreJoueur1G, nombreJoueur1M, nombreJoueur1P, nombreJoueur2G, nombreJoueur2M, nombreJoueur2P
    if partie_en_cours == True : # Si partie _en cours
        posX = (event.x - 15) // 100 # Récupération des coordonnées du clic
        posY = (event.y - 15) // 100
        if (posX >= 3 or posX < 0) and (posY >= 3 or posY < 0) : # Si coordonnées pas dans les normes
            pass # On passe
        else : # Si coordonnées dans les normes
            if liste_joueurs [0].tour == 1 : # Si c'est au tour du premier joueur
                if liste_joueurs [0].couleur == "BLEU" : # Si couleur bleue
                    if tailleJoueur1 == "G" and nombreJoueur1G > 0 and tableau_jeu [posY] [posX] // 100 == 0 : # Si grande pièce choisie et non présente dans la case
                        tableau_jeu [posY] [posX] += 100 # On la positionne dans la case
                        nombreJoueur1G -= 1 # On diminue le nombre de grande pièces du joueur
                        for i in range (3) : # On retire une grande pièce de la réserve
                            if tableau_bleu [i] >= 100 :
                                tableau_bleu [i] -= 100
                                break
                        affichage_bleu () # On affiche la réserve
                        affichage_jeu () # On affiche le jeu
                        gagnant = verif_gagne (liste_joueurs [0].couleur) # On vérifie si le joueur à gagner
                        if gagnant == False : # si non, on change de tour
                            changement_tour ()
                        else : # Si oui
                            liste_joueurs [0].incremente_manche (1) # On incrémente le nombre de manches gagnées
                            affichage_manche_joueur1 () # On affiche les manches
                            gagne_manche ("joueur1") # On affiche le Toplevel de gain
                    elif tailleJoueur1 == "M" and nombreJoueur1M > 0 : # Idem pour pièce moyenne
                        valeur = str(tableau_jeu [posY] [posX]).zfill (3)
                        if valeur [1] == "0" :
                            tableau_jeu [posY] [posX] += 10
                            nombreJoueur1M -= 1
                            for i in range (3) :
                                val = str (tableau_bleu [i]).zfill (3)
                                if val [1] == "1" :
                                    tableau_bleu [i] -= 10
                                    break
                            affichage_bleu ()
                            affichage_jeu ()
                            gagnant = verif_gagne (liste_joueurs [0].couleur)
                            if gagnant == False :
                                changement_tour ()
                            else :
                                liste_joueurs [0].incremente_manche (1)
                                affichage_manche_joueur1 ()
                                gagne_manche ("joueur1")
                    elif tailleJoueur1 == "P" and nombreJoueur1P > 0 : # Idem pour petite pièce
                        valeur = str (tableau_jeu [posY] [posX]).zfill (3)
                        if valeur [2] == "0" :
                            tableau_jeu [posY] [posX] += 1
                            nombreJoueur1P -= 1
                            for i in range (3) :
                                val = str (tableau_bleu [i]).zfill (3)
                                if val [2] == "1" :
                                    tableau_bleu [i] -= 1
                                    break
                            affichage_bleu ()
                            affichage_jeu ()
                            gagnant = verif_gagne (liste_joueurs [0].couleur)
                            if gagnant == False :
                                changement_tour ()
                            else :
                                liste_joueurs [0].incremente_manche (1)
                                affichage_manche_joueur1 ()
                                gagne_manche ("joueur1")
                elif liste_joueurs [0].couleur == "VERT" : # Si couleur verte, même principe que pour bleue mais vérification plus de pièces pour nullité
                    if tailleJoueur1 == "G" and nombreJoueur1G > 0 and tableau_jeu [posY] [posX] // 100 == 0 :
                        tableau_jeu [posY] [posX] += 200
                        nombreJoueur1G -= 1
                        for i in range (3) :
                            if tableau_vert [i] >= 200 :
                                tableau_vert [i] -= 200
                                break
                        affichage_vert ()
                        affichage_jeu ()
                        gagnant = verif_gagne (liste_joueurs [0].couleur)
                        if gagnant == False : # Si coup non gagnant
                            if nombreJoueur1G + nombreJoueur1M + nombreJoueur1P == 0 : # Si plus de pièces vertes à jouer, cas de nullité
                                manche_nulle ()
                            else :
                                changement_tour ()
                        else :
                            liste_joueurs [0].incremente_manche (1)
                            affichage_manche_joueur1 ()
                            gagne_manche ("joueur1")
                    elif tailleJoueur1 == "M" and nombreJoueur1M > 0 :
                        valeur = str (tableau_jeu [posY] [posX]).zfill (3)
                        if valeur [1] == "0" :
                            tableau_jeu [posY] [posX] += 20
                            nombreJoueur1M -= 1
                            for i in range (3) :
                                val = str (tableau_vert [i]).zfill (3)
                                if val [1] == "2" :
                                    tableau_vert [i] -= 20
                                    break
                            affichage_vert ()
                            affichage_jeu ()
                            gagnant = verif_gagne (liste_joueurs [0].couleur)
                            if gagnant == False :
                                if nombreJoueur1G + nombreJoueur1M + nombreJoueur1P == 0 :
                                    manche_nulle ()
                                else :
                                    changement_tour ()
                            else :
                                liste_joueurs [0].incremente_manche (1)
                                affichage_manche_joueur1 ()
                                gagne_manche ("joueur1")
                    elif tailleJoueur1 == "P" and nombreJoueur1P > 0 :
                        valeur = str(tableau_jeu [posY] [posX]).zfill (3)
                        if valeur [2] == "0" :
                            tableau_jeu [posY] [posX] += 2
                            nombreJoueur1P -= 1
                            for i in range (3) :
                                val = str(tableau_vert [i]).zfill (3)
                                if val [2] == "2" :
                                    tableau_vert [i] -= 2
                                    break
                            affichage_vert ()
                            affichage_jeu ()
                            gagnant = verif_gagne (liste_joueurs [0].couleur)
                            if gagnant == False :
                                if nombreJoueur1G + nombreJoueur1M + nombreJoueur1P == 0 :
                                    manche_nulle ()
                                else :
                                    changement_tour ()
                            else :
                                liste_joueurs [0].incremente_manche (1)
                                affichage_manche_joueur1 ()
                                gagne_manche ("joueur1")
            elif liste_joueurs [1].tour == 1 : # Si c'est au tour du second joueur, même principe que pour 1er joueur
                if liste_joueurs [1].couleur == "BLEU" :
                    if tailleJoueur2 == "G" and nombreJoueur2G >0 and tableau_jeu [posY] [posX] // 100 == 0 :
                        tableau_jeu [posY] [posX] += 100
                        nombreJoueur2G -= 1
                        for i in range (3) :
                            if tableau_bleu [i] >= 100 :
                                tableau_bleu [i] -= 100
                                break
                        affichage_bleu ()
                        affichage_jeu ()
                        gagnant = verif_gagne (liste_joueurs [1].couleur)
                        if gagnant == False :
                            changement_tour ()
                        else :
                            liste_joueurs [1].incremente_manche (1)
                            affichage_manche_joueur2 ()
                            gagne_manche ("joueur2")
                    elif tailleJoueur2 == "M" and nombreJoueur2M > 0 :
                        valeur = str (tableau_jeu [posY] [posX]).zfill (3)
                        if valeur [1] == "0" :
                            tableau_jeu [posY] [posX] += 10
                            nombreJoueur2M -= 1
                            for i in range (3) :
                                val = str (tableau_bleu [i]).zfill (3)
                                if val [1] == "1" :
                                    tableau_bleu [i] -= 10
                                    break
                            affichage_bleu ()
                            affichage_jeu ()
                            gagnant = verif_gagne (liste_joueurs [1].couleur)
                            if gagnant == False :
                                changement_tour ()
                            else :
                                liste_joueurs [1].incremente_manche (1)
                                affichage_manche_joueur2 ()
                                gagne_manche ("joueur2")
                    elif tailleJoueur2 == "P" and nombreJoueur2P > 0 :
                        valeur = str (tableau_jeu [posY] [posX]).zfill (3)
                        if valeur [2] == "0" :
                            tableau_jeu [posY] [posX] += 1
                            nombreJoueur2P -= 1
                            for i in range (3) :
                                val = str (tableau_bleu [i]).zfill (3)
                                if val [2] == "1" :
                                    tableau_bleu [i] -= 1
                                    break
                            affichage_bleu ()
                            affichage_jeu ()
                            gagnant = verif_gagne (liste_joueurs [1].couleur)
                            if gagnant == False :
                                changement_tour ()
                            else :
                                liste_joueurs [1].incremente_manche (1)
                                affichage_manche_joueur2 ()
                                gagne_manche ("joueur2")
                elif liste_joueurs [1].couleur == "VERT" : 
                    if tailleJoueur2 == "G" and nombreJoueur2G >0 and tableau_jeu [posY] [posX] // 100 == 0 :
                        tableau_jeu [posY] [posX] += 200
                        nombreJoueur2G -= 1
                        for i in range (3) :
                            if tableau_vert [i] >= 200 :
                                tableau_vert [i] -= 200
                                break
                        affichage_vert ()
                        affichage_jeu ()
                        gagnant = verif_gagne (liste_joueurs [1].couleur)
                        if gagnant == False :
                            if nombreJoueur1G + nombreJoueur1M + nombreJoueur1P == 0 :
                                manche_nulle ()
                            else :
                                changement_tour ()
                        else :
                            liste_joueurs [1].incremente_manche (1)
                            affichage_manche_joueur2 ()
                            gagne_manche ("joueur2")
                    elif tailleJoueur2 == "M" and nombreJoueur2M > 0 :
                        valeur = str(tableau_jeu [posY] [posX]).zfill (3)
                        if valeur [1] == "0" :
                            tableau_jeu [posY] [posX] += 20
                            nombreJoueur2M -= 1
                            for i in range (3) :
                                val = str (tableau_vert [i]).zfill (3)
                                if val [1] == "2" :
                                    tableau_vert [i] -= 20
                                    break
                            affichage_vert ()
                            affichage_jeu ()
                            gagnant = verif_gagne (liste_joueurs [1].couleur)
                            if gagnant == False :
                                if nombreJoueur1G + nombreJoueur1M + nombreJoueur1P == 0 :
                                    manche_nulle ()
                                else :
                                    changement_tour ()
                            else :
                                liste_joueurs [1].incremente_manche (1)
                                affichage_manche_joueur2 ()
                                gagne_manche ("joueur2")
                    elif tailleJoueur2 == "P" and nombreJoueur2P > 0 :
                        valeur = str (tableau_jeu [posY] [posX]).zfill (3)
                        if valeur [2] == "0" :
                            tableau_jeu [posY] [posX] += 2
                            nombreJoueur2P -= 1
                            for i in range (3) :
                                val = str (tableau_vert [i]).zfill (3)
                                if val [2] == "2" :
                                    tableau_vert [i] -= 2
                                    break
                            affichage_vert ()
                            affichage_jeu ()
                            gagnant = verif_gagne (liste_joueurs [1].couleur)
                            if gagnant == False :
                                if nombreJoueur1G + nombreJoueur1M + nombreJoueur1P == 0 :
                                    manche_nulle ()
                                else :
                                    changement_tour ()
                            else :
                                liste_joueurs [1].incremente_manche (1)
                                affichage_manche_joueur2 ()
                                gagne_manche ("joueur2")

def gagne_manche (joueur) :
    ''' Toplevel d'avertissement si manche gagnée '''
    global liste_joueurs, partie_en_cours
    fenGagne = Toplevel (fen, bg = "#00be00")
    fenGagne.resizable(height=False,width=False)
    fenGagne.title ("MORPIOTRIO - Gain de manche")
    fenGagne.geometry ("858x370+531+96")
    frame_gagne_titre = Frame (fenGagne, bg = "#00be00", highlightthickness = 0, height = 128, width = 838)
    frame_gagne_titre.grid (row = 0, column = 0, columnspan = 3, padx = 10, pady = 10)
    frame_gagne_titre.grid_propagate (0)
    canvas_gagne_logo_gauche = Canvas (frame_gagne_titre, bg = "#00be00", bd = 0, highlightthickness = 0, width = 128, height = 128)
    canvas_gagne_logo_gauche.grid (row = 0, column = 0, padx= 0, pady = 0)
    canvas_gagne_logo_gauche.create_image (0, 0, image = imgLogo, anchor = 'nw')
    label_gagne_titre = ttk.Label (frame_gagne_titre, style = "BW.TLabel", text = "MorpioTrio\nGain de la manche", width = 24)
    label_gagne_titre.configure (font = fonte3, background = '#00be00')
    label_gagne_titre.grid (row = 0, column = 1, padx = 25, pady = 0)
    canvas_gagne_logo_droite = Canvas (frame_gagne_titre, bg = "#00be00", bd = 0, highlightthickness = 0, width = 128, height = 128)
    canvas_gagne_logo_droite.grid (row = 0, column = 2, padx= 0, pady = 0)
    canvas_gagne_logo_droite.create_image (0, 0, image = imgLogo, anchor = 'nw')
    label_gagne_info = ttk.Label (fenGagne, style = "BW.TLabel", text = "MorpioTrio\nGain de la manche", width = 50)
    label_gagne_info.grid (row = 1, column = 0, columnspan = 3, pady = 30)
    btManchePlus = ttk.Button (fenGagne, style = "BW.TButton", text = "MANCHE SUIVANTE", width = 17, cursor = "hand2", command = lambda : [nouvelle_manche (), fenGagne.destroy ()])
    btManchePlus.grid (row = 2, column = 0, columnspan = 3, pady = 30)
    btFinPartie = ttk.Button (fenGagne, style = "BW.TButton", text = "FIN DE PARTIE", width = 17, cursor = "hand2", command = lambda : [retour_menu (), fenGagne.destroy ()])
    btFinPartie.grid (row = 2, column = 0, columnspan = 3, pady = 30)
    if joueur == "joueur1" : # Si joueur 1
        if liste_joueurs [0].manches < 3 : # Si manches gagnées inférieures à 3, partie non gagnée
            txtGain = liste_joueurs[0].nom + " a remporté la manche.\n"
            txtGain += "Passer à la manche suivante !"
            label_gagne_info.configure (text = txtGain, font = fonte2, background = "#00be00")
            btManchePlus.grid () # Bouton passage manche suivante activé
            btFinPartie.grid_remove () # Bouton fin de partie désactivé
        else : # Si manches gagnées = 3, partie gagnée
            partie_en_cours = False # On rend la partie non en cours
            txtGain = liste_joueurs[0].nom + " a remporté la manche et la partie.\n"
            txtGain += "Retourner au menu !"
            label_gagne_info.configure (text = txtGain, font = fonte2, background = "#00be00")
            btManchePlus.grid_remove () # Bouton passage manche suivante désactivé
            btFinPartie.grid ()# Bouton fin de partie sactivé
    elif joueur == "joueur2" : # Si joueur 2, même principe que joueur 1
        if liste_joueurs [1].manches < 3 :
            txtGain = liste_joueurs[1].nom + " a remporté la manche.\n"
            txtGain += "Passer à la manche suivante !"
            label_gagne_info.configure (text = txtGain, font = fonte2, background = "#00be00")
            btManchePlus.grid ()
            btFinPartie.grid_remove ()
        else :
            txtGain = liste_joueurs[1].nom + " a remporté la manche et la partie.\n"
            txtGain += "Retourner au menu !"
            label_gagne_info.configure (text = txtGain, font = fonte2, background = "#00be00")
            btManchePlus.grid_remove ()
            btFinPartie.grid ()
    fenGagne.grab_set() # Rend le toplevel maître
    fenGagne.focus () # Donne le focus au Toplevel
    fenGagne.protocol ("WM_DELETE_WINDOW", cross_closing_windows) # Empêche fermeture du Toplevel via la croix

def manche_nulle () :
    ''' Toplevel d'avertissement si manche nulle '''
    global liste_joueurs, partie_en_cours
    fenNulle = Toplevel (fen, bg = "#00be00")
    fenNulle.resizable(height=False,width=False)
    fenNulle.title ("MORPIOTRIO - Manche Nulle")
    fenNulle.geometry ("858x370+531+96")
    frame_nulle_titre = Frame (fenNulle, bg = "#00be00", highlightthickness = 0, height = 128, width = 838)
    frame_nulle_titre.grid (row = 0, column = 0, columnspan = 3, padx = 10, pady = 10)
    frame_nulle_titre.grid_propagate (0)
    canvas_nulle_logo_gauche = Canvas (frame_nulle_titre, bg = "#00be00", bd = 0, highlightthickness = 0, width = 128, height = 128)
    canvas_nulle_logo_gauche.grid (row = 0, column = 0, padx= 0, pady = 0)
    canvas_nulle_logo_gauche.create_image (0, 0, image = imgLogo, anchor = 'nw')
    label_nulle_titre = ttk.Label (frame_nulle_titre, style = "BW.TLabel", text = "MorpioTrio\nManche Nulle", width = 24)
    label_nulle_titre.configure (font = fonte3, background = '#00be00')
    label_nulle_titre.grid (row = 0, column = 1, padx = 25, pady = 0)
    canvas_nulle_logo_droite = Canvas (frame_nulle_titre, bg = "#00be00", bd = 0, highlightthickness = 0, width = 128, height = 128)
    canvas_nulle_logo_droite.grid (row = 0, column = 3, padx= 0, pady = 0)
    canvas_nulle_logo_droite.create_image (0, 0, image = imgLogo, anchor = 'nw')
    label_nulle_info = ttk.Label (fenNulle, style = "BW.TLabel", text = "MorpioTrio\nGain de la manche", width = 50)
    label_nulle_info.grid (row = 1, column = 0, columnspan = 3, pady = 30)
    btManchePlusN = ttk.Button (fenNulle, style = "BW.TButton", text = "MANCHE SUIVANTE", width = 17, cursor = "hand2", command = lambda : [nouvelle_manche (), fenNulle.destroy ()])
    btManchePlusN.grid (row = 2, column = 0, columnspan = 3, pady = 30)
    txtNulle = " Plus de pièce à poser et égalité sur la manche !!\n"
    txtNulle += "Passer à la manche suivante !"
    label_nulle_info.configure (text = txtNulle, font = fonte2, background = "#00be00")
    fenNulle.grab_set() # Rend le toplevel maître
    fenNulle.focus () # Donne le focus au Toplevel
    fenNulle.protocol ("WM_DELETE_WINDOW", cross_closing_windows) # Empêche fermeture du Toplevel via la croix

def verif_gagne (couleur) :
    ''' Fonction de vérification si manche gagnée'''
    global tableau_jeu
    gagne = False
    if couleur == "BLEU" : # Si couleur bleue
        ## Vérification horizontale
        for y in range (3) :
            txt1 = str (tableau_jeu [y] [0]).zfill (3)
            txt2 = str (tableau_jeu [y] [1]).zfill (3)
            txt3 = str (tableau_jeu [y] [2]).zfill (3)
            # Même taille
            if txt1 [0] == "1" and txt2 [0] == "1" and txt3 [0] == "1" :
                gagne = True
                return gagne
                break
            elif txt1 [1] == "1" and txt2 [1] == "1" and txt3 [1] == "1" :
                gagne = True
                return gagne
                break
            elif txt1 [2] == "1" and txt2 [2] == "1" and txt3 [2] == "1" :
                gagne = True
                return gagne
                break
            # Ordre croissant ou décroissant
            elif txt1 [0] == "1" and txt2 [1] == "1" and txt3 [2] == "1" :
                gagne = True
                return gagne
                break
            elif txt1 [2] == "1" and txt2 [1] == "1" and txt3 [0] == "1" :
                gagne = True
                return gagne
                break
        ## Vérification verticale
        for x in range (3) :
            txt1 = str (tableau_jeu [0] [x]).zfill (3)
            txt2 = str (tableau_jeu [1] [x]).zfill (3)
            txt3 = str (tableau_jeu [2] [x]).zfill (3)
            # Même taille
            if txt1 [0] == "1" and txt2 [0] == "1" and txt3 [0] == "1" :
                gagne = True
                return gagne
                break
            elif txt1 [1] == "1" and txt2 [1] == "1" and txt3 [1] == "1" :
                gagne = True
                return gagne
                break
            elif txt1 [2] == "1" and txt2 [2] == "1" and txt3 [2] == "1" :
                gagne = True
                return gagne
                break
            # Ordre croissant ou décroissant
            elif txt1 [0] == "1" and txt2 [1] == "1" and txt3 [2] == "1" :
                gagne = True
                return gagne
                break
            elif txt1 [2] == "1" and txt2 [1] == "1" and txt3 [0] == "1" :
                gagne = True
                return gagne
                break
        ## Vérification diagonale HG -> BD
        # Même taille
        txt1 = str (tableau_jeu [0] [0]).zfill (3)
        txt2 = str (tableau_jeu [1] [1]).zfill (3)
        txt3 = str (tableau_jeu [2] [2]).zfill (3)
        # Même taille
        if txt1 [0] == "1" and txt2 [0] == "1" and txt3 [0] == "1" :
            gagne = True
            return gagne
        elif txt1 [1] == "1" and txt2 [1] == "1" and txt3 [1] == "1" :
            gagne = True
            return gagne
        elif txt1 [2] == "1" and txt2 [2] == "1" and txt3 [2] == "1" :
            gagne = True
            return gagne
        # Ordre croissant ou décroissant
        elif txt1 [0] == "1" and txt2 [1] == "1" and txt3 [2] == "1" :
            gagne = True
            return gagne
        elif txt1 [2] == "1" and txt2 [1] == "1" and txt3 [0] == "1" :
            gagne = True
            return gagne
        ## Vérification diagonale HD -> BG
        # Même taille
        txt1 = str (tableau_jeu [0] [2]).zfill (3)
        txt2 = str (tableau_jeu [1] [1]).zfill (3)
        txt3 = str (tableau_jeu [2] [0]).zfill (3)
        # Même taille
        if txt1 [0] == "1" and txt2 [0] == "1" and txt3 [0] == "1" :
            gagne = True
            return gagne
        elif txt1 [1] == "1" and txt2 [1] == "1" and txt3 [1] == "1" :
            gagne = True
            return gagne
        elif txt1 [2] == "1" and txt2 [2] == "1" and txt3 [2] == "1" :
            gagne = True
            return gagne
        # Ordre croissant ou décroissant
        elif txt1 [0] == "1" and txt2 [1] == "1" and txt3 [2] == "1" :
            gagne = True
            return gagne
        elif txt1 [2] == "1" and txt2 [1] == "1" and txt3 [0] == "1" :
            gagne = True
            return gagne
        ## Vérification sur chaque case
        for y in range (3) :
            for x in range (3) :
                if tableau_jeu [y] [x] == 111 :
                    gagne = True
                    return gagne
                    break
    elif couleur == "VERT" : # Si couleur verte, même principe
        ## Vérification horizontale
        for y in range (3) :
            txt1 = str (tableau_jeu [y] [0]).zfill (3)
            txt2 = str (tableau_jeu [y] [1]).zfill (3)
            txt3 = str (tableau_jeu [y] [2]).zfill (3)
            # Même taille
            if txt1 [0] == "2" and txt2 [0] == "2" and txt3 [0] == "2" :
                gagne = True
                return gagne
                break
            elif txt1 [1] == "2" and txt2 [1] == "2" and txt3 [1] == "2" :
                gagne = True
                return gagne
                break
            elif txt1 [2] == "2" and txt2 [2] == "2" and txt3 [2] == "2" :
                gagne = True
                return gagne
                break
            # Ordre croissant ou décroissant
            elif txt1 [0] == "2" and txt2 [1] == "2" and txt3 [2] == "2" :
                gagne = True
                return gagne
                break
            elif txt1 [2] == "2" and txt2 [1] == "2" and txt3 [0] == "2" :
                gagne = True
                return gagne
                break
        ## Vérification verticale
        for x in range (3) :
            txt1 = str (tableau_jeu [0] [x]).zfill (3)
            txt2 = str (tableau_jeu [1] [x]).zfill (3)
            txt3 = str (tableau_jeu [2] [x]).zfill (3)
            # Même taille
            if txt1 [0] == "2" and txt2 [0] == "2" and txt3 [0] == "2" :
                gagne = True
                return gagne
                break
            elif txt1 [1] == "2" and txt2 [1] == "2" and txt3 [1] == "2" :
                gagne = True
                return gagne
                break
            elif txt1 [2] == "2" and txt2 [2] == "2" and txt3 [2] == "2" :
                gagne = True
                return gagne
                break
            # Ordre croissant ou décroissant
            elif txt1 [0] == "2" and txt2 [1] == "2" and txt3 [2] == "2" :
                gagne = True
                return gagne
                break
            elif txt1 [2] == "2" and txt2 [1] == "2" and txt3 [0] == "2" :
                gagne = True
                return gagne
                break
        ## Vérification diagonale HG -> BD
        # Même taille
        txt1 = str (tableau_jeu [0] [0]).zfill (3)
        txt2 = str (tableau_jeu [1] [1]).zfill (3)
        txt3 = str (tableau_jeu [2] [2]).zfill (3)
        # Même taille
        if txt1 [0] == "2" and txt2 [0] == "2" and txt3 [0] == "2" :
            gagne = True
            return gagne
        elif txt1 [1] == "2" and txt2 [1] == "2" and txt3 [1] == "2" :
            gagne = True
            return gagne
        elif txt1 [2] == "2" and txt2 [2] == "2" and txt3 [2] == "2" :
            gagne = True
            return gagne
        # Ordre croissant ou décroissant
        elif txt1 [0] == "2" and txt2 [1] == "2" and txt3 [2] == "2" :
            gagne = True
            return gagne
        elif txt1 [2] == "2" and txt2 [1] == "2" and txt3 [0] == "2" :
            gagne = True
            return gagne
        ## Vérification diagonale HD -> BG
        # Même taille
        txt1 = str (tableau_jeu [0] [2]).zfill (3)
        txt2 = str (tableau_jeu [1] [1]).zfill (3)
        txt3 = str (tableau_jeu [2] [0]).zfill (3)
        # Même taille
        if txt1 [0] == "2" and txt2 [0] == "2" and txt3 [0] == "2" :
            gagne = True
            return gagne
        elif txt1 [1] == "2" and txt2 [1] == "2" and txt3 [1] == "2" :
            gagne = True
            return gagne
        elif txt1 [2] == "2" and txt2 [2] == "2" and txt3 [2] == "2" :
            gagne = True
            return gagne
        # Ordre croissant ou décroissant
        elif txt1 [0] == "2" and txt2 [1] == "2" and txt3 [2] == "2" :
            gagne = True
            return gagne
        elif txt1 [2] == "2" and txt2 [1] == "2" and txt3 [0] == "2" :
            gagne = True
            return gagne
        ## Vérification sur chaque case
        for y in range (3) :
            for x in range (3) :
                if tableau_jeu [y] [x] == 222 :
                    gagne = True
                    return gagne
                    break
    return gagne

def affichage_manche_joueur1 () :
    ''' Procédure d'affichage des manches gagnées par premier joueur '''
    global liste_joueurs
    canvas_joueur1_manche.delete (ALL)
    if liste_joueurs [0].manches == 0 :
        canvas_joueur1_manche.create_image (0, 0, image = imgM0, anchor = "nw")
    elif liste_joueurs [0].manches == 1 :
        canvas_joueur1_manche.create_image (0, 0, image = imgM1, anchor = "nw")
    elif liste_joueurs [0].manches == 2 :
        canvas_joueur1_manche.create_image (0, 0, image = imgM2, anchor = "nw")
    elif liste_joueurs [0].manches == 3 :
        canvas_joueur1_manche.create_image (0, 0, image = imgM3, anchor = "nw")

def affichage_manche_joueur2 () :
    ''' Procédure d'affichage des manches gagnées par second joueur '''
    global liste_joueurs
    canvas_joueur2_manche.delete (ALL)
    if liste_joueurs [1].manches == 0 :
        canvas_joueur2_manche.create_image (0, 0, image = imgM0, anchor = "nw")
    elif liste_joueurs [1].manches == 1 :
        canvas_joueur2_manche.create_image (0, 0, image = imgM1, anchor = "nw")
    elif liste_joueurs [1].manches == 2 :
        canvas_joueur2_manche.create_image (0, 0, image = imgM2, anchor = "nw")
    elif liste_joueurs [1].manches == 3 :
        canvas_joueur2_manche.create_image (0, 0, image = imgM3, anchor = "nw")

def affichage_jeu () :
    ''' Procédure d'affichage du jeu '''
    global partie_en_cours, tableau_jeu
    if partie_en_cours == True : # Si partie en cours
        canvas_jeu_jeu.delete (ALL) # On efface le canvas
        canvas_jeu_jeu.create_image (0, 0, image = imgFond, anchor = "nw") # On y place le fond
        for y in range (3) :
            for x in range (3) : # Pour chaque case, on place les éventuelles pièces placées (bleue ou verte, petite, moyenne et/ou grande)
                valeur_case = tableau_jeu [y] [x] // 100
                if valeur_case == 2 :
                    canvas_jeu_jeu.create_image (15 + x*100, 15+ y*100, image = imgGCV, anchor = 'nw')
                elif valeur_case == 1 :
                    canvas_jeu_jeu.create_image (15 + x*100, 15+ y*100, image = imgGCB, anchor = 'nw')
                valeur_case = tableau_jeu [y] [x]
                while valeur_case > 100 :
                    valeur_case -= 100
                valeur_case = valeur_case // 10
                if valeur_case == 2 :
                    canvas_jeu_jeu.create_image (15 + x*100, 15+ y*100, image = imgMCV, anchor = 'nw')
                elif valeur_case == 1 :
                    canvas_jeu_jeu.create_image (15 + x*100, 15+ y*100, image = imgMCB, anchor = 'nw')
                valeur_case = tableau_jeu [y] [x]
                while valeur_case > 100 :
                    valeur_case -= 100
                valeur_case = valeur_case % 10
                if valeur_case == 2 :
                    canvas_jeu_jeu.create_image (15 + x*100, 15+ y*100, image = imgPCV, anchor = 'nw')
                elif valeur_case == 1 :
                    canvas_jeu_jeu.create_image (15 + x*100, 15+ y*100, image = imgPCB, anchor = 'nw')

def affichage_bleu () :
    ''' Procédure d'affichage des pièces bleues disponibles dans leur réserve '''
    global tableau_bleu, partie_en_cours
    canvas_reserve_bleu.delete (ALL) # On vide le canvas
    canvas_reserve_bleu.create_image (0, 0, image= imgReserve, anchor = "nw") # On y place le fond
    for i in range (3) : # Pour chaque case, on place les pièces disponibles
        if tableau_bleu [i] == 111 :
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgGCB, anchor = "nw")
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgMCB, anchor = "nw")
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgPCB, anchor = "nw")
        elif tableau_bleu [i] == 110 :
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgGCB, anchor = "nw")
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgMCB, anchor = "nw")
        elif tableau_bleu [i] == 101 :
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgGCB, anchor = "nw")
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgPCB, anchor = "nw")
        elif tableau_bleu [i] == 100 :
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgGCB, anchor = "nw")
        elif tableau_bleu [i] == 11 :
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgMCB, anchor = "nw")
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgPCB, anchor = "nw")
        elif tableau_bleu [i] == 10 :
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgMCB, anchor = "nw")
        elif tableau_bleu [i] == 1 :
            canvas_reserve_bleu.create_image (15 + i*100, 15, image = imgPCB, anchor = "nw")

def affichage_vert () :
    ''' Procédure d'affichage des pièces vertes disponibles dans leur réserve (idem que pour pièces bleues) '''
    global tableau_vert, partie_en_cours
    canvas_reserve_vert.delete (ALL)
    canvas_reserve_vert.create_image (0, 0, image= imgReserve, anchor = "nw")
    for i in range (3) :
        if tableau_vert [i] == 222 :
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgGCV, anchor = "nw")
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgMCV, anchor = "nw")
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgPCV, anchor = "nw")
        elif tableau_vert [i] == 220 :
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgGCV, anchor = "nw")
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgMCV, anchor = "nw")
        elif tableau_vert [i] == 202 :
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgGCV, anchor = "nw")
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgPCV, anchor = "nw")
        elif tableau_vert [i] == 200 :
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgGCV, anchor = "nw")
        elif tableau_vert [i] == 22 :
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgMCV, anchor = "nw")
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgPCV, anchor = "nw")
        elif tableau_vert [i] == 20 :
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgMCV, anchor = "nw")
        elif tableau_vert [i] == 2 :
            canvas_reserve_vert.create_image (15 + i*100, 15, image = imgPCV, anchor = "nw")

def nouvelle_manche () :
    ''' Procédure pour débuter une nouvelle manche '''
    global liste_joueurs, tableau_bleu, tableau_bleu_original, tableau_jeu, tableau_jeu_original, tableau_vert, tableau_vert_original
    global nombreJoueur1G, nombreJoueur1M, nombreJoueur1P, nombreJoueur2G, nombreJoueur2M, nombreJoueur2P, tailleJoueur1, tailleJoueur2
    tableau_bleu = copy.deepcopy (tableau_bleu_original) # On remet le tableau de réserve bleu au départ
    tableau_vert = copy.deepcopy (tableau_vert_original) # On remet le tableau de réserve vert au départ
    tableau_jeu = copy.deepcopy (tableau_jeu_original) # On remet le tableau de jeu au départ
    # On affiche les réserves et le jeu
    affichage_bleu ()
    affichage_vert ()
    affichage_jeu ()
    # On affiche les manches gagnées pour chaque joueur
    affichage_manche_joueur1 ()
    affichage_manche_joueur2 ()
    # On change la couleur et le tour de chaque joueur
    liste_joueurs [0].change_couleur ()
    liste_joueurs [1].change_couleur ()
    # On remet la taille de sélection des pièces à grande pour chaque joueur
    tailleJoueur1 = "G"
    tailleJoueur2 = "G"
    # On remet le nombre de chaque pièces disponibles à 3 pour chaque joueur
    nombreJoueur1G = 3
    nombreJoueur1M = 3
    nombreJoueur1P = 3
    nombreJoueur2G = 3
    nombreJoueur2M = 3
    nombreJoueur2P = 3
    # On rempli les canvas de sélection pour chaque joueur
    canvas_joueur1_selection.delete (ALL)
    canvas_joueur2_selection.delete (ALL)
    if liste_joueurs [0].couleur == "VERT" :
        canvas_joueur1_selection.create_image (0, 0, image = imgGCV, anchor = "nw")
        canvas_joueur1_selection.configure (state = DISABLED)
    elif liste_joueurs [0].couleur == "BLEU" :
        canvas_joueur1_selection.create_image (0, 0, image = imgGCB, anchor = "nw")
        canvas_joueur1_selection.configure (state = NORMAL)
    if liste_joueurs [1].couleur == "VERT" :
        canvas_joueur2_selection.create_image (0, 0, image = imgGCV, anchor = "nw")
        canvas_joueur2_selection.configure (state = DISABLED)
    elif liste_joueurs [1].couleur == "BLEU" :
        canvas_joueur2_selection.create_image (0, 0, image = imgGCB, anchor = "nw")
        canvas_joueur2_selection.configure (state = NORMAL)
    # On remplit le label d'information précisant quel joueur joue
    if liste_joueurs [0].tour == 1 and liste_joueurs [1].tour == 0 :
        label_jeu_info.configure (text = "\nAU TOUR DE " + liste_joueurs [0].nom + " DE JOUER !\n")
    elif liste_joueurs [0].tour == 0 and liste_joueurs [1].tour == 1 :
        label_jeu_info.configure (text = "\nAU TOUR DE " + liste_joueurs [1].nom + " DE JOUER !\n")

def nouvelle_partie () :
    ''' Procédure pour débuter une nouvelle partie '''
    global liste_joueurs, tableau_bleu, tableau_bleu_original, tableau_jeu, tableau_jeu_original, tableau_vert, tableau_vert_original, partie_en_cours
    # On récupère le nom des joueurs
    nom1 = nomValue1.get ()
    nom2 = nomValue2.get ()
    if nom1 == "" : # Si Pas de nom pour le premier joueur
        showerror ("Nom manquant !","Il manque le nom du premier joueur !!") # On prévient que joueur non inscrit
        entry_inscription_joueur_1.focus_set () # On met le focus sur l'entry du premier joueur
        return # On abandonne la procédure
    elif nom2 == "" : # Si pas de nom pour le deuxième joueur
        showerror ("Nom manquant !","Il manque le nom du second joueur !!") # On prévient que joueur non inscrit
        entry_inscription_joueur_2.focus_set () # On met le focus sur l'entry du second joueur
        return # On abandonne la procédure
    else : # Si un nom par joueur
        if nom2 == nom1 : # Si même nom que le premier joueur
            showerror ("Même noms !","Le second joueur à le même nom que le premier !!\n\nMerci de choisir un autre nom !!") # On prévient que joueur non inscrit
            entry_inscription_joueur_2.focus_set () # On met le focus sur l'entry du second joueur
            entry_inscription_joueur_2.select_range(0, END) # On sélectionne l'intégralité du widget
            return # On abandonne la procédure
        else : # Sinon
            liste_joueurs [:] = [] # On vide la liste des joueurs
            # On met le nom des joueurs en majuscule
            nom1 = nom1.upper ()
            nom2 = nom2.upper ()
            tirage = randint (1,100) # On tire un nombre entre un et 100
            if tirage <= 50 : # Si nombre inférieur ou égal à 100
                coul1 = "VERT" # Le premier joueur joue avec les pions verts
                tour1 = 0 # Ce n'est pas au tour du premier joueur de jouer
                coul2 = "BLEU" # Le second joueur joue avec les pions bleus
                tour2 = 1 # C'est au tour du second joueur de jouer
            else :
                coul1 = "BLEU" # Le premier joueur joue avec les pions bleus
                tour1 = 1 # C'est au tour du premier joueur de jouer
                coul2 = "VERT" # Le second joueur joue avec les pions verts
                tour2 = 0 # Ce n'est pas au tour du second joueur de jouer
            partie_en_cours = True
            liste_joueurs.append (Joueurs (nom = nom1, couleur = coul1, manches = 0, tour = tour1)) # Ajout du premier joueur à la liste
            liste_joueurs.append (Joueurs (nom = nom2, couleur = coul2, manches = 0, tour = tour2)) # Ajout du second joueur à la liste
            nouvelle_manche () # On remet les tableaux aux départ et on inverse les joueurs
            frame_menu.grid_remove () # On cache la frame de menu
            frame_jeu.grid () # On rend la frame de jeu visible
            label_joueur1_nom.configure (text = liste_joueurs [0].nom) # On met le nom du premier joueur
            label_joueur1_couleur.configure (text = liste_joueurs [0].couleur)
            label_joueur2_nom.configure (text = liste_joueurs [1].nom) # On met le nom du second joueur
            label_joueur2_couleur.configure (text = liste_joueurs [1].couleur)
            if liste_joueurs [0].tour == 1 :
                label_jeu_info.configure (text = "\nAU TOUR DE " + liste_joueurs [0].nom + " DE JOUER !\n")
            elif liste_joueurs [1].tour == 1 :
                label_jeu_info.configure (text = "\nAU TOUR DE " + liste_joueurs [1].nom + " DE JOUER !\n")
## Fin fonctions et procédures

## Création de la fenêtre
fen = Tk()
## Fin création de la fenêtre

## Variables et images
# VARIABLES
fonte1 = ('Arial',16, 'bold')
fonte2 = ('Arial', 20, 'bold')
fonte3 = ('Arial', 30, 'bold')
fonte4 = ('Arial', 50, 'bold')
nomValue1 = StringVar ()
nomValue1.trace ('w', limitNom)
nomValue2 = StringVar ()
nomValue2.trace ('w', limitNom)
liste_joueurs = []
tableau_jeu = []
tableau_jeu_original =[[0,0,0],[0,0,0],[0,0,0]]
tableau_bleu = []
tableau_bleu_original = [111,111,111]
tableau_vert = []
tableau_vert_original = [222,222,222]
partie_en_cours = False
tableau_jeu = copy.deepcopy (tableau_jeu_original)
tableau_bleu = copy.deepcopy (tableau_bleu_original)
tableau_vert = copy.deepcopy (tableau_vert_original)
tailleJoueur1 = "G"
tailleJoueur2 = "G"
nombreJoueur1G = 3
nombreJoueur1M = 3
nombreJoueur1P = 3
nombreJoueur2G = 3
nombreJoueur2M = 3
nombreJoueur2P = 3
# IMAGES
imgFond = PhotoImage (file = 'images\\fond.png')
imgReserve = PhotoImage (file = 'images\\fond reserve h.png')
imgDepart = PhotoImage (file = 'images\\fond depart.png')
imgGCB = PhotoImage (file = 'images\\cercle bleu grand.png')
imgMCB = PhotoImage (file = 'images\\cercle bleu moyen.png')
imgPCB = PhotoImage (file = 'images\\cercle bleu petit.png')
imgGCV = PhotoImage (file = 'images\\cercle vert grand.png')
imgMCV = PhotoImage (file = 'images\\cercle vert moyen.png')
imgPCV = PhotoImage (file = 'images\\cercle vert petit.png')
imgM0 = PhotoImage (file = 'images\\manche 0.png')
imgM1 = PhotoImage (file = 'images\\manche 1.png')
imgM2 = PhotoImage (file = 'images\\manche 2.png')
imgM3 = PhotoImage (file = 'images\\manche 3.png')
imgG3PVD = PhotoImage (file = 'images\\gain 3pvd.png')
imgG3VDH = PhotoImage (file = 'images\\gain 3vdh.png')
imgG3BCV = PhotoImage (file = 'images\\gain 3bcv.png')
imgG3BMC = PhotoImage (file = 'images\\gain 3bmc.png')
imgNG = PhotoImage (file = 'images\\no gain.png')
imgLogo = PhotoImage (file = 'images\\logo 128.png')
## Fin variables et images

## Styles
s = ttk.Style ()
s.theme_use ()
s.map ("BW.TButton", background = [('focus', 'yellow'), ('!focus', 'blue')])
s.configure ("BW.TButton", font = fonte1, background = 'cyan', foreground = 'purple', borderwidht = 0, anchor = CENTER, justify = CENTER)
s.configure ("BW.TLabel", font = fonte1, background = 'olive', foreground = 'white', justify = CENTER, highlightthickness = 0, anchor = CENTER, border = 0)
## Fin styles

## Intérieur fenêtre
# 0. Généralités
fen.title ("MORPIOTRIO  ¦¦  VERSION 2 JOUEURS")
fen.resizable (height= False, width = False)
fen.configure (bg = 'olive')
if sys.platform.startswith ('linux') :
    fen.iconphoto (True, PhotoImage (file = 'images\\logo.xbm'))
elif sys.platform.startswith ('win32') :
    fen.iconphoto (True, PhotoImage (file = 'images\\logo.png'))
# 1. Menu
frame_menu = Frame (fen, bg = "olive", highlightthickness = 0, height = 854, width = 858)
frame_menu.grid (row = 0, column = 0)
frame_menu.grid_propagate (0)
frame_menu_titre = Frame (frame_menu, bg = "olive", highlightthickness = 0)
frame_menu_titre.grid (row = 0, column = 0, columnspan = 3, padx = 10, pady = 10)
canvas_menu_logo_gauche = Canvas (frame_menu_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_menu_logo_gauche.grid (row = 0, column = 0, padx= 0, pady = 0)
canvas_menu_logo_gauche.create_image (0, 0, image = imgLogo, anchor ='nw')
label_menu_titre = ttk.Label (frame_menu_titre, style = "BW.TLabel", text = "MorpioTrio", width = 14)
label_menu_titre.configure (font = fonte4)
label_menu_titre.grid (row = 0, column = 1, padx = 30, pady = 0)
canvas_menu_logo_droite = Canvas (frame_menu_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_menu_logo_droite.grid (row = 0, column = 2, padx= 0, pady = 0)
canvas_menu_logo_droite.create_image (0, 0, image = imgLogo, anchor ='nw')
canvas_menu_depart = Canvas (frame_menu_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 165, height = 295)
canvas_menu_depart.grid (row = 1, column = 1, pady = 36)
canvas_menu_depart.create_image (0, 0, image = imgDepart, anchor = 'nw')
frame_menu_inscription = LabelFrame(frame_menu, bg='olive', fg = "white", bd = 3, relief = RIDGE, labelanchor='n',text='Joueurs', font = fonte1, width = 896)
frame_menu_inscription.grid (row = 2, column = 0, columnspan = 3,padx = 10, pady = 36)
entry_inscription_joueur_1 = Entry (frame_menu_inscription, width = 14, font = fonte1, textvariable = nomValue1, justify = CENTER, fg ="purple", highlightthickness = 2, highlightcolor = "purple", highlightbackground = "purple")
entry_inscription_joueur_1.grid(row = 0, column = 0, padx = 10, pady = 10)
entry_inscription_joueur_2 = Entry (frame_menu_inscription, width = 14, font = fonte1, textvariable = nomValue2, justify = CENTER, fg ="purple",  highlightthickness = 2, highlightcolor = "purple", highlightbackground = "purple")
entry_inscription_joueur_2.grid(row = 0, column = 1, padx = 10, pady = 10)
frame_menu_boutons = Frame (frame_menu, bg = 'olive', bd = 3, relief = RIDGE)
frame_menu_boutons.grid (row = 3, column = 0, columnspan = 3, padx = 10, pady = 36)
btNP = ttk.Button (frame_menu_boutons, style = "BW.TButton", text = "NOUVELLE PARTIE", width = 17, cursor = "hand2", command = nouvelle_partie)
btNP.grid (row = 0, column = 0, padx = 20, pady = 10)
btQuitter = ttk.Button (frame_menu_boutons, style = "BW.TButton", text = "QUITTER", width = 17, cursor = "hand2", command = fen.destroy)
btQuitter.grid (row = 1, column = 2, padx = 20, pady = 10)
btAide = ttk.Button (frame_menu_boutons, style = "BW.TButton", text = "AIDE", width = 17, cursor = "hand2", command = menu_aide)
btAide.grid (row = 1, column = 0, padx = 20, pady = 10)
btAP = ttk.Button (frame_menu_boutons, style = "BW.TButton", text = "À PROPOS", width = 17,cursor = "hand2", command = menu_AP)
btAP.grid (row = 0, column = 2, padx = 20, pady = 10)
entry_inscription_joueur_1.insert (0, "JOUEUR 1")
entry_inscription_joueur_2.insert (0, "JOUEUR 2")
entry_inscription_joueur_1.focus_set ()
entry_inscription_joueur_1.select_range (0, END) # On sélectionne l'intégralité du widget
# 2. Jeu
frame_jeu = Frame (fen, bg = "olive", highlightthickness = 0, height = 854, width = 858)
frame_jeu.grid (row = 0, column = 0)
frame_jeu.grid_propagate (0)
frame_jeu_titre = Frame (frame_jeu, bg = "olive", highlightthickness = 0)
frame_jeu_titre.grid (row = 0, column = 0, columnspan = 3, padx = 10, pady = 10)
canvas_jeu_logo_gauche = Canvas (frame_jeu_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_jeu_logo_gauche.grid (row = 0, column = 0, padx= 0, pady = 0)
canvas_jeu_logo_gauche.create_image (0, 0, image = imgLogo, anchor = 'nw')
label_jeu_titre = ttk.Label (frame_jeu_titre, style = "BW.TLabel", text = "MorpioTrio", width = 14)
label_jeu_titre.configure (font = fonte4)
label_jeu_titre.grid (row = 0, column = 1, padx = 30, pady = 0)
canvas_jeu_logo_droite = Canvas (frame_jeu_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_jeu_logo_droite.grid (row = 0, column = 2, padx= 0, pady = 0)
canvas_jeu_logo_droite.create_image (0, 0, image = imgLogo, anchor = 'nw')
frame_jeu_canvas = Frame (frame_jeu, bg = "olive", highlightthickness = 0)
frame_jeu_canvas.grid (row = 1, column = 1, pady = 10)
canvas_reserve_bleu = Canvas (frame_jeu_canvas, bg = "olive", bd = 0, highlightthickness = 0, width = 330, height = 130)
canvas_reserve_bleu.grid (row = 0, column = 0)
canvas_reserve_bleu.create_image (0, 0, image = imgReserve, anchor = "nw")
canvas_jeu_jeu = Canvas (frame_jeu_canvas, bg = "olive", bd = 0, highlightthickness = 0, cursor ="hand2", width = 330, height = 330)
canvas_jeu_jeu.grid (row = 1, column = 0)
canvas_jeu_jeu.create_image (0, 0, image = imgFond, anchor = "nw")
canvas_reserve_vert = Canvas (frame_jeu_canvas, bg = "olive", bd = 0, highlightthickness = 0, width = 330, height = 130)
canvas_reserve_vert.grid (row = 2, column = 0)
canvas_reserve_vert.create_image (0, 0, image = imgReserve, anchor = "nw")
affichage_jeu ()
affichage_bleu ()
affichage_vert ()
frame_jeu_joueur1 = Frame (frame_jeu, bg = "olive", highlightthickness = 0, bd = 4, relief = RIDGE)
frame_jeu_joueur1.grid (row = 1, column = 0, padx = 10, pady = 10)
label_joueur1_nom = ttk.Label (frame_jeu_joueur1, style = "BW.TLabel", text = "JOUEUR 1111", width = 14)
label_joueur1_nom.grid (row = 0, column = 0, padx = 5, pady = 10)
label_joueur1_couleur = ttk.Label (frame_jeu_joueur1, style = "BW.TLabel", text = "BLEU", width = 12)
label_joueur1_couleur.grid (row = 1, column = 0, padx = 5, pady = 10)
canvas_joueur1_manche = Canvas (frame_jeu_joueur1, bg = "white", bd = 0, highlightthickness = 0, width = 120, height = 40)
canvas_joueur1_manche.grid (row = 2, column = 0, padx = 5, pady = 10)
canvas_joueur1_manche.create_image (0, 0, image = imgM0, anchor = "nw")
canvas_joueur1_selection = Canvas (frame_jeu_joueur1, bg = "white", bd = 0, highlightthickness = 0, cursor ="hand2", width = 100, height = 100)
canvas_joueur1_selection.grid (row = 3, column = 0, pady = 10)
canvas_joueur1_selection.create_image (0, 0, image = imgGCB, anchor = "nw")
frame_jeu_joueur2 = Frame (frame_jeu, bg = "olive", highlightthickness = 0, bd = 4, relief = RIDGE)
frame_jeu_joueur2.grid (row = 1, column = 2, padx = 10, pady = 10)
label_joueur2_nom = ttk.Label (frame_jeu_joueur2, style = "BW.TLabel", text = "JOUEUR 2222", width = 14)
label_joueur2_nom.grid (row = 0, column = 0, padx = 5, pady = 10)
label_joueur2_couleur = ttk.Label (frame_jeu_joueur2, style = "BW.TLabel", text = "VERT", width = 12)
label_joueur2_couleur.grid (row = 1, column = 0, padx = 5, pady = 10)
canvas_joueur2_manche = Canvas (frame_jeu_joueur2, bg = "white", bd = 0, highlightthickness = 0, width = 120, height = 40)
canvas_joueur2_manche.grid (row = 2, column = 0, padx = 5, pady = 10)
canvas_joueur2_manche.create_image (0, 0, image = imgM0, anchor = "nw")
canvas_joueur2_selection = Canvas (frame_jeu_joueur2, bg = "white", bd = 0, highlightthickness = 0, cursor ="hand2", width = 100, height = 100)
canvas_joueur2_selection.grid (row = 3, column = 0, pady = 10)
canvas_joueur2_selection.create_image (0, 0, image = imgGCV, anchor = "nw")
canvas_joueur2_selection.configure (state = DISABLED)
label_jeu_info = ttk.Label (frame_jeu, style = "BW.TLabel", text = "\nAU TOUR DE JOUEUR 111 DE JOUER !\n", width = 36)
label_jeu_info.grid (row = 2, column = 1, pady = 10)
label_jeu_info.configure (background = "cyan", foreground = "purple", border = 4, relief = RIDGE)
frame_jeu.grid_remove ()
# 3. À PROPOS
frame_ap = Frame (fen, bg = "olive", highlightthickness = 0, height = 854, width = 858)
frame_ap.grid (row = 0, column = 0)
frame_ap.grid_propagate (0)
frame_ap_titre = Frame (frame_ap, bg = "olive", highlightthickness = 0)
frame_ap_titre.grid (row = 0, column = 0, columnspan = 3, padx = 10, pady = 10)
canvas_ap_logo_gauche = Canvas (frame_ap_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_ap_logo_gauche.grid (row = 0, column = 0, padx= 0, pady = 0)
canvas_ap_logo_gauche.create_image (0, 0, image = imgLogo, anchor = 'nw')
label_ap_titre = ttk.Label (frame_ap_titre, style = "BW.TLabel", text = "MorpioTrio", width = 14)
label_ap_titre.configure (font = fonte4)
label_ap_titre.grid (row = 0, column = 1, padx = 30, pady = 0)
canvas_ap_logo_droite = Canvas (frame_ap_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_ap_logo_droite.grid (row = 0, column = 2, padx= 0, pady = 0)
canvas_ap_logo_droite.create_image (0, 0, image = imgLogo, anchor = 'nw')
label_titre_ap = ttk.Label (frame_ap, style = "BW.TLabel", text = "À PROPOS", width = 10)
label_titre_ap. grid (row = 1, column = 1, pady = 65)
label_titre_ap.configure (font = fonte3)
label_info_ap = ttk.Label (frame_ap, style = "BW.TLabel", text = "")
label_info_ap.grid (row = 2, column = 0, columnspan = 3, pady = 66)
txtAP = "© copyleft - Bruno CLÉVENOT - Mars 2023\n\n"
txtAP += "Jeu programmé en python 3.7 par Bruno CLÉVENOT.\n\n"
txtAP += "Graphismes par Bruno CLÉVENOT.\n\n"
txtAP += "Code et graphismes distribués sous licence GPL 3."
label_info_ap.configure (text = txtAP, font = fonte2, justify = LEFT)
btApMenu = ttk.Button (frame_ap, style = "BW.TButton", text = " MENU ", cursor ="hand2", command = ap_menu)
btApMenu.grid (row = 3, column = 1, pady = 66)
frame_ap.grid_remove ()
# 4. Aide
frame_aide = Frame (fen, bg = "olive", highlightthickness = 0, height = 854, width = 858)
frame_aide.grid (row = 0, column = 0)
frame_aide.grid_propagate (0)
frame_aide_titre = Frame (frame_aide, bg = "olive", highlightthickness = 0)
frame_aide_titre.grid (row = 0, column = 0, columnspan = 3, padx = 10, pady = 10)
canvas_aide_logo_gauche = Canvas (frame_aide_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_aide_logo_gauche.grid (row = 0, column = 0, padx= 0, pady = 0)
canvas_aide_logo_gauche.create_image (0, 0, image = imgLogo, anchor = 'nw')
label_aide_titre = ttk.Label (frame_aide_titre, style = "BW.TLabel", text = "MorpioTrio", width = 14)
label_aide_titre.configure (font = fonte4)
label_aide_titre.grid (row = 0, column = 1, padx = 30, pady = 0)
canvas_aide_logo_droite = Canvas (frame_aide_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_aide_logo_droite.grid (row = 0, column = 2, padx= 0, pady = 0)
canvas_aide_logo_droite.create_image (0, 0, image = imgLogo, anchor = 'nw')
label_titre_aide = ttk.Label (frame_aide, style = "BW.TLabel", text = "AIDE", width = 10)
label_titre_aide. grid (row = 1, column = 1, pady = 27)
label_titre_aide.configure (font = fonte3)
label_info_aide = ttk.Label (frame_aide, style = "BW.TLabel", text = "")
label_info_aide.grid (row = 2, column = 0, columnspan = 3, pady = 27)
txtAide = "But :\nAligner trois de ces pièces :\n"
txtAide += "  • de même taille (horizontalement, verticalement ou diagonalement).\n"
txtAide += "  • par taille croissante ou décroissante (horizontalement, verticalement ou\n    diagonalement).\n"
txtAide += "  • sur la même case.\n\n"
txtAide += "Contraintes :\n"
txtAide += "• Les 'bleus' commencent toujours la manche en cours.\n"
txtAide += "• Chaque joueur dispose de 9 pièces : 3 grandes, 3 moyennes et 3 petites.\n"
txtAide += "• À son tour de jouer, le joueur sélectionne la taille du pion à placer en cliquant sur\n"
txtAide += "  sa case de taille (en bas de sa feuille de marque), puis sur une case du plateau\n"
txtAide += "  central où cette pièce peut être placée (case vide pour la taille choisie).\n"
txtAide += "• Chaque case du plateau central peut accueillir une pièce de chaque taille (de\n"
txtAide += "  même couleur ou de couleurs différentes).\n"
txtAide += "• Si les 2 joueurs ont placé toutes leurs pièces sans qu'aucun n'est réussi à fournir\n"
txtAide += "  une condition gagnante, la manche est considérée comme nulle.\n"
txtAide += "• Il faut remporter 3 manches pour gagner la partie.\n"
txtAide += "• À chaque changement de manche, les joueurs inversent leurs couleurs."
label_info_aide.configure (text = txtAide, justify = LEFT)
frame_aide_boutons = Frame (frame_aide, bg = "olive", highlightthickness = 0)
frame_aide_boutons.grid (row = 3, column = 0, columnspan = 3, pady = 27)
btAideMenu = ttk.Button (frame_aide_boutons, style = "BW.TButton", text = " MENU ", cursor ="hand2", command = aide_menu)
btAideMenu.grid (row = 0, column = 0, padx = 30)
btAideExemple = ttk.Button (frame_aide_boutons, style = "BW.TButton", text = "  EXEMPLES DE GAINS  ", cursor ="hand2", command = aide_exemple)
btAideExemple.grid (row = 0, column = 1, padx = 30)
frame_aide.grid_remove ()
# 5. Exemple
frame_exemple = Frame (fen, bg = "olive", highlightthickness = 0, height = 854, width = 858)
frame_exemple.grid (row = 0, column = 0)
frame_exemple.grid_propagate (0)
frame_exemple_titre = Frame (frame_exemple, bg = "olive", highlightthickness = 0)
frame_exemple_titre.grid (row = 0, column = 0, columnspan = 3, padx = 10, pady = 10)
canvas_exemple_logo_gauche = Canvas (frame_exemple_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_exemple_logo_gauche.grid (row = 0, column = 0, padx= 0, pady = 0)
canvas_exemple_logo_gauche.create_image (0, 0, image = imgLogo, anchor = 'nw')
label_exemple_titre = ttk.Label (frame_exemple_titre, style = "BW.TLabel", text = "MorpioTrio", width = 14)
label_exemple_titre.configure (font = fonte4)
label_exemple_titre.grid (row = 0, column = 1, padx = 30, pady = 0)
canvas_exemple_logo_droite = Canvas (frame_exemple_titre, bg = "olive", bd = 0, highlightthickness = 0, width = 128, height = 128)
canvas_exemple_logo_droite.grid (row = 0, column = 2, padx= 0, pady = 0)
canvas_exemple_logo_droite.create_image (0, 0, image = imgLogo, anchor = 'nw')
label_titre_exemple = ttk.Label (frame_exemple, style = "BW.TLabel", text = "EXEMPLES", width = 10)
label_titre_exemple. grid (row = 1, column = 1, pady = 6)
label_titre_exemple.configure (font = fonte3)
frame_exemple_info = Frame (frame_exemple, bg = "olive", highlightthickness = 0)
frame_exemple_info.grid (row = 2, column = 0, columnspan = 3, pady = 6)
canvas_exemple_info1 = Canvas (frame_exemple_info, bg = "olive", bd = 0, highlightthickness = 0, width = 110, height = 110)
canvas_exemple_info1.grid (row = 0 , column = 0, padx =10)
canvas_exemple_info1.create_image (0, 0, image = imgG3PVD, anchor = "nw")
label_exemple_info1 = ttk.Label (frame_exemple_info, style = "BW.TLabel", text = "Victoire des verts par alignement\nde 3 pièces de même taille.")
label_exemple_info1.grid (row = 0, column = 1, padx = 10)
label_exemple_info1.configure (justify = LEFT)
canvas_exemple_info2 = Canvas (frame_exemple_info, bg = "olive", bd = 0, highlightthickness = 0, width = 110, height = 110)
canvas_exemple_info2.grid (row = 1 , column = 0, padx =10, pady = 6)
canvas_exemple_info2.create_image (0, 0, image = imgG3BCV, anchor = "nw")
label_exemple_info2 = ttk.Label (frame_exemple_info, style = "BW.TLabel", text = "Victoire des bleus par alignement\nde 3 pièces par ordre croissant.")
label_exemple_info2.grid (row = 1, column = 1, padx = 10, pady = 6)
label_exemple_info2.configure (justify = LEFT)
canvas_exemple_info3 = Canvas (frame_exemple_info, bg = "olive", bd = 0, highlightthickness = 0, width = 110, height = 110)
canvas_exemple_info3.grid (row = 2 , column = 0, padx =10)
canvas_exemple_info3.create_image (0, 0, image = imgG3VDH, anchor = "nw")
label_exemple_info3 = ttk.Label (frame_exemple_info, style = "BW.TLabel", text = "Victoire des verts par alignement\nde 3 pièces par ordre décroissant.")
label_exemple_info3.grid (row = 2, column = 1, padx = 10)
label_exemple_info3.configure (justify = LEFT)
canvas_exemple_info4 = Canvas (frame_exemple_info, bg = "olive", bd = 0, highlightthickness = 0, width = 110, height = 110)
canvas_exemple_info4.grid (row = 3 , column = 0, padx =10, pady = 6)
canvas_exemple_info4.create_image (0, 0, image = imgG3BMC, anchor = "nw")
label_exemple_info4 = ttk.Label (frame_exemple_info, style = "BW.TLabel", text = "Victoire des bleus par alignement\nde 3 pièces sur une même case.")
label_exemple_info4.grid (row = 3, column = 1, padx = 10, pady = 6)
label_exemple_info4.configure (justify = LEFT)
canvas_exemple_info5 = Canvas (frame_exemple_info, bg = "olive", bd = 0, highlightthickness = 0, width = 110, height = 110)
canvas_exemple_info5.grid (row = 4 , column = 0, padx =10)
canvas_exemple_info5.create_image (0, 0, image = imgNG, anchor = "nw")
label_exemple_info5 = ttk.Label (frame_exemple_info, style = "BW.TLabel", text = "Pas de victoire des bleus : les 3\npièces ne sont pas de même taille\net ne sont pas par ordre croissant\nou décroissant.")
label_exemple_info5.grid (row = 4, column = 1, padx = 10)
label_exemple_info5.configure (justify = LEFT)
btExempleRetour = ttk.Button (frame_exemple, style = "BW.TButton", text = " RETOUR ", cursor ="hand2", command = exemple_aide)
btExempleRetour.grid (row = 3, column = 1, pady = 6)
frame_exemple.grid_remove ()
## Fin intérieur fenêtre

## Placement de la fenêtre
fen.update ()
w = fen.winfo_width ()
h = fen.winfo_height ()
ws = fen.winfo_screenwidth ()
hs = fen.winfo_screenheight ()
a = (ws - w) // 2
b = (hs - h -34) // 2
fen.geometry ("%dx%d+%d+%d" % (w, h, a, b))
## Fin placement de la fenêtre

## Fonction de fermeture de la fenêtre
fen.protocol ("WM_DELETE_WINDOW", quitter_jeu)
## Fin fonction fermeture de fenêtre

## Fonction de bin des canvas
canvas_joueur1_selection.bind ('<Button-1>', choix_joueur1)
canvas_joueur2_selection.bind ('<Button-1>', choix_joueur2)
canvas_jeu_jeu.bind ('<Button-1>', placement)
## Fin fonction bind

fen.mainloop ()
``` 