# Planning and evaluation

You have been asked to **build a ray tracer from first principles**, using the C++ programming language.

{% hint style="warning" %}
The goal of this project is to develop your engineering skills, your ability to design and execute complex software development. The following are therefore considered contrary to the spirit of the exercise and will not be allowed or accepted:

* Copying or adapting, in any way, existing ray tracer repositories on Git-Hub or elsewhere.
* Using Chat-GPT, or any other artificial intelligence, to write your code.

I will frequently ask you to explain your code, and you will be penalized if you cannot sufficiently explain your data structure or algorithms.
{% endhint %}


## Calendar


| Date                                                              | Theme              | Format| For Evaluation |
| ------------------------------------------------------------------- | ----------------- | -- | -- |
| Tuesday 28 October, morning | Client needs & technical brief |
| Tuesday 28 October, afternoon | Vision and strategy | Course + discussion (1 hour) |
| Wednesday 29 October | Piloting a technical project | Course + discussion (1 hour) |
| Friday 31 October | Evaluation 1: Vision & Strategy  | Group meeting | Yes |
| Monday 3 November | Work at Hetic, presence for questions and answers | | 
| Tuesday 4 November | Progress meeting (obligatory) | | Yes |  
| Friday 7 November | Presentation of final project | Group evaluation in the form of a Client Presentation | Yes |
| - | | |
| Monday 1 December | New engineering theme related to the Raytracer |  | |
| Monday 1 December | Individual Code Reviews for the RayTracer (evaluation) | Code Review | Yes |
| Tuesday 2 December | Delivery of Technical Poster | PDF, or SVG | Yes |
| 1 - 5 December | Individual work on evolving the Raytracer | Courses, exercises and Katas | Yes |


## Deliverables

- **Friday 31 October** : the PDF containing your Vision, [described here](../concepts/vision.md#exercise-for-evaluation)  
- **Friday 7 October** : Your final presentation package for the client
- **Monday 1 December** : Code Review, in person, where you choose a part of your code and present it to me
- **Tuesday 2 December** : the PDF containing your Technical Poster [described here](../concepts/vision.md#exercise-for-evaluation)  


The final **presentation package** must consist of the following: 
* The image(s) rendered by your software (ready to be transferred as a .zip file)
* A table describing an analysis of the performance of your software (total rendering time of your image(s))
* You will be asked to render an image live in front of the client
* A link to the GitHub project
* A link to your JIRA



**Notation of the final product**

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

