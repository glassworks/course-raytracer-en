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

You must work in teams of maximum 4 people. [Please specify your teams here.](https://docs.google.com/spreadsheets/d/1qHr7hSANnmTzyi69LXJbhnVzSG8Ipa5p9VCVnAoc07s/edit?usp=sharing)

## Evaluation

You have been asked to **build a ray tracer from first principles**, using the C++ programming language.

{% hint style="warning" %}
The goal of this project is to develop your engineering skills, your ability to design and execute complex software development. The following are therefore considered contrary to the spirit of the exercise and will not be allowed or accepted:

* Copying or adapting, in any way, existing ray tracer repositories on Git-Hub or elsewhere.
* Using Chat-GPT, or any other artificial intelligence, to write your code.

I will frequently ask you to explain your code, and you will be penalized if you cannot sufficiently explain your data structure or algorithms.
{% endhint %}

**Delivery and deliverables**

You will be required to present your software on Friday, 7 November, 2025. You will be required to present the following:
* The image(s) rendered by your software
* The total rendering time of your image(s)
* You will be asked to render an image live in front of the client
* You will be required to present and explain parts of your code
* You must provide a link to the GitHub project

**Notation**

Scoring is done à la carte. A functional minimum viable product (MVP) will earn you a passing score. You are then free to implement any techniques you wish to improve your score, up to a maximum of 20 points.

The following rating scale will be used to evaluate the project:

| Aspect                                                              | Note              |
| ------------------------------------------------------------------- | ----------------- |
| **Functional base product**                                   |                   |
| A functional C++ executable                                       | 1                 |
| A PNG image is produced                                          | 1                 |
| At a minimum, flat rendering of a sphere is achieved                  | 1                 |
| At a minimum, diffuse rendering of a sphere is achieved                | 2                 |
| Rendering of a plane                                                     | 1                 |
| Reflections                                                          | 2                 |
| **C++ architecture and code quality**                             |                   |
| Data structures                                               | 1                 |
| Clean code                                                          | 1                 |
| Algorithms used and correctly explained                      | 1                 |
| **Additional points**                                          |                   |
| Surface shaders other than diffuse shaders                | 3                 |
| Rendering of other shapes                                               | 3                 |
| Rendering of a 3D model (.obj, .fbx, etc.)                              | 3                 |
| Optimization strategy                                            |  up to 8 points |
| Advanced surface rendering techniques                             | 3                 |
| Structured scene modeling language                       | 2                 |
| Any other feature that is sufficiently explained and implemented | 3                 |
