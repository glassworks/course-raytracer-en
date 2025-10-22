---
cover: >-
  https://images.unsplash.com/photo-1515922912707-dbc512030899?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw4fHxzcGhlcmV8ZW58MHx8fHwxNzI5MzA4NTk3fDA&ixlib=rb-4.0.3&q=85
coverY: 0
---

# Overview

The goal of this cycle is to introduce you to **advanced software engineering**. In your career as a Tech Lead/CTO, you will be asked to design and develop software that goes beyond a simple website or web application with a database, API and front-end.
- You will need to develop a **strategic vision**, encompassing :
  - A vision of the final project you are aiming to produce
  - A vision of how the project is to be run
  - A vision of the ressources (time, financial, etc.) needed 
- You will need to **innovate** :
  - Be confronted with difficulties and unknowns, and come up with creative solutions
  - Extract and anticipate client needs and propose creative solutions
- You will need to **drive and execute** a technically difficult project
- You will need to **manage a technical team**

## Context

As a software engineer, you will often be asked to model a scientific principle, a mathematical principle, or emulate physics-based behaviors. All this with the aim of creating a useful tool for your customers. This task can often be daunting:

* You will need to learn and understand mathematical, physical, or other technical concepts that are outside your comfort zone.
* You will need to translate these concepts into your field: data structures, algorithms, architecture, etc.
* You will need to overcome performance issues
* You will need to deliver a product that is truly useful to your customer

For this project, we are throwing you in at the deep end and asking you to design complex mathematical software! This isn't because we're sadistic; in fact, there are a number of really important and useful skills that should result from this exercise:

* The ability to translate a mathematical principle into an engineering problem
* Choosing and implementing good data structures, design patterns, and adopting a clean architecture.
* Adding a programming language to your toolbox (if you don't already know C++)
* Facing serious optimization problems and trying to find solutions.
* Striving to create a pleasant user experience.

This is a group project, and as a result, as a future Tech Lead/CTO, you will also need to practice and refine your non-technical, but nonetheless essential, skills:
* Working and coordinating with other developers (planning, delegation, synchronization, conflict resolution, etc.). You are free to use the project management philosophy of your choice (Agile, Scrum, Kanban, etc.).
* Working with a centralized GIT repository
* Code review among colleagues


## The project : Ray Tracer

It's 2035. AI and Chat-GPT have destroyed the market for technical skills. An entire generation of "vibe-coders" has given rise to a multitude of flawed software versions. The giants of computer image rendering are on their knees. Adobe and Autodesk have gone bankrupt. Blender has become unusable.

The major 3D computer graphics studios are desperate—they need their software to produce their next film and have nowhere to turn! Fortunately, you are here to save the day!

Your mission is to create, from first principles, a **ray tracer**: software that renders 3D images by simulating how light bounces around a scene.

<figure><img src=".gitbook/assets/test.png" alt=""><figcaption><p>Example of a scene rendered by a basic raytracer with 4 levels of reflection. There is room for improvement!</p></figcaption></figure>

You have two weeks to develop this software. Our client, a renowned LA based film studio, requires the following features:

* Render at least one **sphere** and one **plane** with full reflection (i.e., a fully metallic sphere that reflects its surroundings), and produce a single image in PNG format.
* You must be able to render a high-resolution image of a scene with a large number of objects and at least 4 light bounces. You must measure the rendering time and include it in your final submission. Remember that a movie is composed of a series of static images. Your software will therefore need to render hundreds of thousands of images to create the movie. **Rendering speed** is therefore an important factor for the client!
* If you succeed, you will receive additional credit for any of the following:
  * Implementing other surface models (Blinn, Phong, Gourad, Cook-Torrance).  
  * Rendering other shapes, such as cubes, cylinders, triangles
  * Rendering a 3D model (in .obj, .fbx, .collada, or other format)
  * Rendering optimization strategies:
    * Space partitioning
    * Multi-threading or parallel processing
    * Use of the GPU
    
   * Multi-processing (rendering on a cluster, queues, etc.)
  * More advanced surface rendering techniques: texture mapping, bump mapping, environment mapping, etc.
  * A structured scene modeling language (an input file?) specifying the layout of the scene
  * Anti-aliasing
  * ...

However, in this dystopian future, there are a few constraints! All modern programming languages such as Go, Python, Java, etc. have become completely proprietary. To use them, you have to pay huge royalties, which will make this project unfeasible. **You must use the only remaining free language: C++**.

Fortunately, there are a few wise elders who can pass on the almost lost knowledge about these fantastic software programs, which has been compiled in this guide. Read this information carefully!

* [What is a ray-tracer ?](raytracer/intro.md)
* [Get started with C++](cpp/intro.md)

## Group project

Vous devez travailler en groupe de maximum 4 personnes. Merci de renseigner la constitution de vos groupes ici : [https://docs.google.com/spreadsheets/d/15XxlY-hAXphluYYi91rkFycaz-DHESSliPAoS5DUFLo/edit?usp=sharing](https://docs.google.com/spreadsheets/d/15XxlY-hAXphluYYi91rkFycaz-DHESSliPAoS5DUFLo/edit?usp=sharing)

## Notation

On vous a demandé de **construire un traceur de rayons à partir des premiers principes**, en utilisant le langage de programmation C++.

{% hint style="warning" %}
Le but de ce projet est de développer vos compétences d'ingénieur, votre capacité à concevoir et à exécuter un développement logiciel complexe. Les éléments suivants sont donc considérés comme contraires à l'esprit de l'exercice, et ne seront pas autorisés ou acceptés :

* La copie ou l'adaptation, de quelque manière que ce soit, des dépôts de traceurs de rayons existants sur Git-Hub ou ailleurs.
* L'utilisation de Chat-GPT, ou d'une autre intelligence artificielle, pour écrire votre code.

Je vous demanderai fréquemment d'expliquer votre code, et vous serez pénalisé si vous ne pouvez pas expliquer suffisamment votre structure de données ou vos algorithmes.
{% endhint %}

**Livraison et livrables**

Vous devrez présenter votre logiciel le jeudi 31 octobre 2024. Vous devrez présenter les éléments suivants :

* la ou les images rendues par votre logiciel
* le temps total de rendu de votre (vos) image(s)
* il vous sera demandé de réaliser un rendu d'image en direct devant le client
* vous devrez présenter et expliquer une partie de votre code
* vous devez fournir un lien vers le projet GitHub

**Notation**

La notation est réalisée _à la carte_. Un produit de base fonctionnel (MVP) vous vaudra une note qui passe. Ensuite, vous êtes libre de mettre en œuvre toutes les techniques que vous souhaitez pour améliorer votre note, jusqu'à un maximum de 20 points.

La grille de notation suivante sera utilisée pour évaluer le projet :

| Aspect                                                              | Note              |
| ------------------------------------------------------------------- | ----------------- |
| **Produit de base fonctionnel**\*                                   |                   |
| Un exécutable C++ fonctionnel                                       | 1                 |
| Une image PNG est produite                                          | 1                 |
| Au minimum, le rendu plat d'une sphère est réalisé                  | 1                 |
| Au minimum, le rendu diffus d'une sphère est réalisé                | 2                 |
| Rendu d'un plan                                                     | 1                 |
| Réflexions                                                          | 2                 |
| **Architecture C++ et qualité du code**                             |                   |
| Structures de données                                               | 1                 |
| Clean code                                                          | 1                 |
| Algorithmes utilisés et correctement expliqués                      | 1                 |
| **Points supplémentaires**                                          |                   |
| Les shaders de surface autres que les shaders diffus                | 3                 |
| Rendu d'autres formes                                               | 3                 |
| Rendu d'un modèle 3D (.obj, .fbx, ...)                              | 3                 |
| Stratégie d'optimisation                                            |  jusqu'à 8 points |
| Techniques avancées de rendu de surface                             | 3                 |
| Langage structuré de modélisation de la scène                       | 2                 |
| Toute autre caractéristique suffisamment expliquée et mise en œuvre | 3                 |
