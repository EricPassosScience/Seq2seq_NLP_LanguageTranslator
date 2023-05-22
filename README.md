# Traductor de idiomas con Machine Learning y NLP

## Modelo Seq2seq 
Google introdujo por primera vez el modelo Seq2seq para la traducción automática. Antes de eso, la traducción funcionaba de forma muy ingenua. Cada palabra que solía escribir se convirtió al idioma de destino, independientemente de la gramática y la estructura de la oración. Seq2seq revolucionó el proceso de traducción utilizando Deep Learning. No solo tiene en cuenta la palabra de entrada actual durante la traducción, sino también su vecindad.

Actualmente se utiliza para una variedad de aplicaciones diferentes, como leyendas de imágenes, plantillas de conversación, resúmenes de texto, traducción, etc.

Como sugiere el nombre, Seq2seq toma una secuencia de palabras (oración u oraciones) como entrada y genera una secuencia de palabras de salida. Lo hace utilizando una red neuronal recurrente (RNN), siendo común el uso de versiones avanzadas de RNN, es decir, LSTM o GRU. Esto se debe a que la RNN sufre el problema de la disipación del gradiente. Se utiliza el modelo LSTM en la versión propuesta por Google. Desarrolla el contexto de la palabra, tomando 2 entradas en cada momento. Uno actual y otro de salida anterior, de ahí el nombre recurrente (salida entra como entrada).

Seq2seq tiene principalmente dos componentes: codificador y decodificador y, por lo tanto, a veces se denomina red de codificador-decodificador.

 - Codificador: utiliza capas de redes neuronales profundas y convierte las palabras de entrada en los vectores ocultos correspondientes. Cada vector representa la palabra actual y el contexto de la palabra.

- Decodificador: Es similar al codificador. Toma como entrada el vector oculto generado por el codificador, sus propios estados ocultos y la palabra actual para producir el siguiente vector oculto y finalmente predecir la siguiente palabra.

Vamos a ver:

![imagem_2023-05-20_134046272](https://github.com/EricPassosScience/NLP_Word2vec_PCA_Visualization/assets/97414922/fe74c9fa-67c7-4f03-b615-0287b58665c2)

Además de estos dos elementos, muchas optimizaciones llevaron a otros componentes de Seq2seq:

- Attention: La entrada al decodificador es un solo vector que debe almacenar toda la información sobre el contexto. Esto se convierte en un problema con secuencias grandes. Por lo tanto, se aplica el mecanismo de atención, lo que permite que el decodificador observe la secuencia de entrada de forma selectiva.

- Beam Search: La palabra con la probabilidad más alta es seleccionada como salida por el decodificador. Pero esto no siempre produce los mejores resultados, debido al problema básico de los algoritmos codiciosos. Por lo tanto, se aplica la búsqueda de haces, que sugiere posibles traducciones en cada paso. Esto se hace creando un árbol de resultados principales.

- Bucketing: Las secuencias de longitud variable son posibles en un modelo Seq2seq, debido al relleno 0 que se realiza en la entrada y la salida. Sin embargo, si la longitud máxima establecida por nosotros es 100 y la oración es de solo 3 palabras, causará una gran pérdida de espacio. Entonces, usamos el concepto de Bucketing. Creamos variables de diferentes tamaños como (4,8)(8,15) y así sucesivamente, donde 4 es la longitud de entrada máxima definida por nosotros y 8 es la longitud de salida máxima definida.

