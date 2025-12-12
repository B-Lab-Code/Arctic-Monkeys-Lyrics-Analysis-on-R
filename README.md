# Arctic-Monkeys-Lyrics-Analysis-on-R

## ¿Que hará este blog? 

Arctic Monkeys es una de las bandas más importantes e icónicas del rock alternativo actual. La primera vez que uno escucha esa batería lenta y pesada sonando con un leve eco al fondo, interrumpida por un ya icónico riff de guitarra que muestra el carácter oscuro y seductor de lo que será ***Do I Wanna Know***, te das cuenta de que ese ritmo se quedará con uno por siempre. 

Sin embargo, hay más canciones que *Do I Wanna Know* y álbumes qué *AM*. Los temas que trata la banda pueden variar según la canción y álbum, por lo que puede ser interesante observar de forma más global que quiere contar cada obra de los *cuatro de Sheffiel*. 

Tomando en cuenta lo anterior, en este blog se quiere mostrar cómo se puede analizar, en un lenguaje de programación como R, la obra musical de la banda. En este caso, más que un ensayo sobre los simbolismos de cada canción se mostrarán los datos “macro” de cada álbum y canción. Se revisará las letras y mostrará si existen patrones según álbum. 

Para esto se usó el dataset llamado *Arctic Monkeys Lyrics*, subido por el usuario GGAPP1 a Kaggle, disponible en el siguiente enlace: 

https://www.kaggle.com/datasets/ggapp1/arctic-monkeys-lyrics 

La última actualización de esta dataset fue antes de la publicación del álbum *The Car* de 2022, ya que este no está incluido. Por esto, se revisarán las canciones hasta el álbum *Tranquility Base Hotel & Casino*. 

A continuación podrán ver como llevar a cabo el proyecto.


<p align="center">↓↓↓ Sigan hacia abajo ↓↓↓</p>



```text

                                                          .;X&&&&&&&&&&X+.                                
                                                   .:x&&&&&&&&&&&&&&&&&&&&&&&&x:.                         
                                                .X&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&X.                      
                                            ..$&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&$:.                  
                                          .;&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&+.                
                                        .+&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&x.              
                                       ;&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&;             
                                      &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&.           
                                    :&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&;          
                                   +&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&x         
                                 .x&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&x.       
                                 +&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&XxX&&&x:...+&&&&&&&x       
                                ;&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&x...&:.    x+  x&x.     ;&&&&&&&&;      
                               .&&&&&&&&&&&&&&&&&&&&&&&&$X;..X&&:     &.   .:x;  XX   .X&&x&&&&&&&&&.     
                               X&&&&&&&&&&&&&&&&&&&X&&$. ..   &.  ;&&&&&+  +&&.  &:   $&&&&&&&&&&&&&X     
                              .&&&&&&&&&&&&&&&&&.  .&&+  x&. .+  .&&&&&&;  x&&. .&;   .$&&&&&&&&&&&&&.    
                              +&&&&&&&&&&&&&&&&: ; .$&:  .  :&;  .$&&+&&:  $&&. ;&&.      ;&&&&&&&&&&+    
                              $&&&&&&&&&&&&&&&. +$  :&. ..  .&&.     .&&. .&&X  x&&&$.   .+&&&&&&&&&&&.   
                              &&&&&&&&&&&&&&&.      .&. .&.  .&&+.  ..&&;+x&&&&&&$$&&$$$&&$X$&&&&&&&&&.   
                              &&&&&&&&&&&&&$. .$&$  .x  :&&&&&&XX$$x+&&::+$    +$. ;$  ;+.   .&&&&&&&&.   
                              &&&&&&&&&&&&&&&&&&&&&Xx&&&&.  X&&. x; .&. +&X .X$&&+ .. .$  ;&&$&&&&&&&&.   
                              &&&&&&&&&$..&&: x&X.    .&$   .&+ .$. .. X&&+ ...&&&.  .&&.   :&&&&&&&&&.   
                              $&&&&&&&&:  ;.  xx  X&&  xx    ;. +x    :&&&. ...&&&+ .&&&&+.   &&&&&&&&.   
                              +&&&&&&&x .. .. x: :&&X  $: :$    X; .x  +&$  .+++&&; .&&&.+x. .&&&&&&&+    
                              .&&&&&&&. $;.$; +x  ..  x&. ;&x   $: .&.  X$     +&&: .&&;    .&&&&&&&&.    
                               X&&&&&;:;&&&&;:x&&;::X&&&:;X&&xxX&$&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&X     
                               .&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&.     
                                ;&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&;      
                                 x&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&x       
                                 .x&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&x.       
                                   +&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&x         
                                    :&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&;          
                                      &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&.           
                                       ;&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&+             
                                        .x&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&x.              
                                          .+&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&+.                
                                            ..$&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&$:.                  
                                                .$&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&$.                      
                                                   .:x&&&&&&&&&&&&&&&&&&&&&&&&x;.                         
                                                        ...+X&&&&&&&&&&X+:..                              
```

## ¿Q? 

La base de datos es bastante simple. Es un archivo .csv que solo tiene tres variables (o columnas) que son:  
- ` name `
- ` album `
- `lyrics `

Si bien, no son tantas, dentro de ` album ` hay cosas que podrían generar “ruido” en el análisis posterior ya que aparecen singles, EPs como *Beneath The Boardwalk*, versiones de radio, etc) 

