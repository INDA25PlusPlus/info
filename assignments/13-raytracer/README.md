# Uppgift 13 - Ray Tracing

## Läxa

Veckans läxa är att implementera någon form av ray tracing algoritm. Programmet
ska antingen visa bilden i ett fönster eller producera bildfiler i något
rimligt format (t.ex BMP, JPG, PNG, etc.). Din raytracer ska kunna hantera
sfärer och oändliga plan, men ni får gärna ha flera typer av objekt. Den
ska också har någon form av belysning. Repot ska ha namnet ha namnet “**_kth-id_**-raytracer”.

Lägg gärna upp bilder på er progress/resultat i discorden.

## Utökningar

* Path tracer
    * Monte carlo metod
    * Objekt är ljuskällor
    * Mycket beräkningar (Rekommenderat att ha algoritmen på GPU eller multithreaded)
* Ray marcher
* Multithreading
* Implementera din algoritm på GPU för att köra snabbare
* Implementera en BVH för att göra algoritmen snabbare
* Textures


## Material

* [Ray Tracing in One Weekend](https://raytracing.github.io/) (superbra utgångspunkt)
* [Intersection equations](https://github.com/INDA24PlusPlus/raytracing-material/blob/main/intersections.pdf)
* [Bounding Volume Hierarchies(BVH)](https://raytracing.github.io/books/RayTracingTheNextWeek.html#boundingvolumehierarchies)
* [Bounding Volume Hierarchies(BVH) serie](https://jacco.ompf2.com/2022/04/13/how-to-build-a-bvh-part-1-basics/)
* [Path tracing](https://raytracing.github.io/books/RayTracingTheRestOfYourLife.html)
* [Ray marching](https://michaelwalczyk.com/blog-ray-marching.html)
* [PPM (lätt bild format om ni inte vill använda bibliotek)](https://en.wikipedia.org/wiki/Netpbm#PPM_example)
