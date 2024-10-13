---
title: 'Salidas Estructuradas con GPT-4o y GPT-4o Mini'
date: '2024-10-12T00:00:00-03:00'
author: 'Rodrigo Juarez'
layout: post
permalink: /2024/10/12/salidas-estructuradas-gpt-4o/
categories:
    - Azure OpenAI
    - AI
---

# Introducción

En una era donde la inteligencia artificial se está volviendo cada vez más integral en diversas industrias, modelos como GPT-4o y GPT-4o Mini están liderando el camino. Estos modelos, especialmente con la actualización de agosto de 2024, no solo son más poderosos sino que también ofrecen características más refinadas. Una de esas características es "Salidas Estructuradas", que está revolucionando cómo se formatean y utilizan las respuestas impulsadas por IA. En este artículo, exploraremos los beneficios de las "Salidas Estructuradas" y proporcionaremos un ejemplo de cómo implementarlas utilizando Azure AI Studio.

## Salidas Estructuradas

En el procesamiento del lenguaje natural tradicional, lograr que un modelo de IA produzca texto similar al humano es solo el comienzo. Para muchas aplicaciones, especialmente en dominios empresariales y técnicos, las respuestas necesitan seguir una estructura específica. Aquí es donde entran en juego las "Salidas Estructuradas", permitiendo respuestas que no solo son contextualmente precisas sino que también están formateadas de una manera que se integra perfectamente con otros sistemas.

Ya sea generando documentos formateados, datos estructurados para bases de datos o plantillas de respuesta específicas para chatbots, las "Salidas Estructuradas" pueden mejorar significativamente la utilidad y eficiencia del contenido generado por IA. La versión de agosto de 2024 de GPT-4o y GPT-4o Mini incorpora capacidades avanzadas para agilizar este proceso, haciendo más fácil que nunca producir salidas consistentes y confiables.

## GPT-4o y GPT-4o Mini: Una Breve Reseña

GPT-4o y GPT-4o Mini son iteraciones del modelo GPT-4 de OpenAI, optimizadas para diversas aplicaciones y restricciones de recursos. Mientras que GPT-4o está diseñado para tareas de gran escala y alta complejidad que requieren un poder computacional extenso, GPT-4o Mini es una versión más compacta y eficiente, adecuada para entornos con recursos limitados sin un sacrificio significativo en el rendimiento.

# Un ejemplo sin Salidas Estructuradas

Podemos generar datos estructurados con un prompt como este

Create a random list of 3 users for mocking purposes, include full name, email, phone, address and username. Format as a Json array.

El payload json enviado al endpoint chat/completions podría ser algo como esto

```
{
    "messages": [
        {
            "role": "user",
            "content": [
                {
                    "type": "text",
                    "text": "Create a random list of 3 users for mocking purposes, include full name, email, phone, address and username. Format as a Json array."
                }
            ]
        }
    ],
    "temperature": 0.7,
    "top_p": 0.95,
    "max_tokens": 800
}
```

Y la respuesta sería algo como esto

```
{
  "message": {
    "content": [
      {
        "full_name": "Emily Johnson",
        "email": "emily.johnson@example.com",
        "phone": "555-123-4567",
        "address": "123 Maple Street, Springfield, IL 62704",
        "username": "emily_j"
      },
      {
        "full_name": "Michael Smith",
        "email": "michael.smith@example.com",
        "phone": "555-234-5678",
        "address": "456 Oak Avenue, Anytown, CA 90210",
        "username": "mike_smith"
      },
      {
        "full_name": "Jessica Brown",
        "email": "jessica.brown@example.com",
        "phone": "555-345-6789",
        "address": "789 Pine Road, Metropolis, NY 10001",
        "username": "jess_brown"
      }
    ],
    "role": "assistant"
  }
}
```

Así es como lo hemos estado usando hasta ahora. Aunque los prompts pueden llevarte lejos, e incluso cuando la salida parece correcta, necesitarás decodificar la respuesta. Por lo general, encontrarás problemas con la adherencia al esquema, la consistencia y el manejo de escenarios complejos.

# Usando Salidas Estructuradas

Ahora, con las nuevas Salidas Estructuradas, podemos usar un esquema JSON para definir el formato de la respuesta. En la siguiente solicitud de API, definimos un array JSON donde los elementos dentro de él son los usuarios. Observa cómo la dirección es un objeto en sí mismo, y aunque no cambiamos el prompt, se rellena en consecuencia. Si tu esquema JSON tiene algún problema, recibirás un mensaje de error en respuesta a tu solicitud.

```
{
    "messages": [
        {
            "role": "user",
            "content": [
                {
                    "type": "text",
                    "text": "Create a random list of 3 users for mocking purposes, include full name, email, phone, address and username."
                }
            ]
        }
    ],
    "temperature": 0.7,
    "top_p": 0.95,
    "max_tokens": 800,
    "response_format": {
        "type": "json_schema",
        "json_schema": {
            "name": "UserList",
            "strict": true,
            "schema": {
                "type": "object",
                "properties": {
                    "users": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "full_name": {
                                    "type": "string"
                                },
                                "email": {
                                    "type": "string"
                                },
                                "phone": {
                                    "type": "string",
                                    "description": "International format, starting with a '+' and country code"
                                },
                                "address": {
                                    "type": "object",
                                    "properties": {
                                        "street_address": {
                                            "type": "string"
                                        },
                                        "city": {
                                            "type": "string"
                                        },
                                        "state": {
                                            "type": "string"
                                        },
                                        "postal_code": {
                                            "type": "string"
                                        },
                                        "country": {
                                            "type": "string"
                                        }
                                    },
                                    "additionalProperties": false,
                                    "required": [
                                        "street_address",
                                        "city",
                                        "state",
                                        "postal_code",
                                        "country"
                                    ]
                                },
                                "username": {
                                    "type": "string"
                                }
                            },
                            "additionalProperties": false,
                            "required": [
                                "full_name",
                                "email",
                                "username",
                                "phone",
                                "address"
                            ]
                        }
                    }
                },
                "required": ["users"],
                "additionalProperties": false
            }
        }
    }
}
```

Y aquí está la sección relevante en la respuesta

```
{
  "message": {
    "content": {
      "users": [
        {
          "full_name": "Olivia Harper",
          "email": "olivia.harper@example.com",
          "phone": "+1-202-555-0131",
          "address": {
            "street_address": "123 Maple Street",
            "city": "Springfield",
            "state": "IL",
            "postal_code": "62701",
            "country": "USA"
          },
          "username": "oharper"
        },
        {
          "full_name": "Liam Chen",
          "email": "liam.chen@example.com",
          "phone": "+44-20-7946-0958",
          "address": {
            "street_address": "456 Elm Road",
            "city": "London",
            "state": "Greater London",
            "postal_code": "SW1A 1AA",
            "country": "UK"
          },
          "username": "lchen"
        },
        {
          "full_name": "Ava Müller",
          "email": "ava.mueller@example.com",
          "phone": "+49-30-1234-5678",
          "address": {
            "street_address": "789 Birkenweg",
            "city": "Berlin",
            "state": "Berlin",
            "postal_code": "10115",
            "country": "Germany"
          },
          "username": "amueller"
        }
      ]
    },
    "role": "assistant"
  }
}
```

Para más detalles sobre el formato necesario y las opciones disponibles en tu esquema Json, consulta los enlaces en la sección de recursos. Estos recursos proporcionan ejemplos y mejores prácticas para ayudar a asegurar que obtengas el resultado deseado.

# Conclusión

La introducción de las "Salidas Estructuradas" en las versiones de agosto de 2024 de GPT-4o y GPT-4o Mini marca un avance significativo en el contenido generado por IA. Al utilizar esquemas JSON para definir los formatos de respuesta, los desarrolladores pueden lograr salidas más precisas, consistentes y confiables. Esta mejora simplifica la integración con otros sistemas y reduce la necesidad de un extenso análisis de datos. A medida que la tecnología de IA progresa, aprovechar características como las "Salidas Estructuradas" será esencial para maximizar la eficiencia y efectividad. Te animamos a explorar estas nuevas capacidades utilizando los recursos proporcionados.

# Recursos
[How to use structured outputs with Azure OpenAI Service – Azure OpenAI | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/structured-outputs?tabs=python-secure)
[Announcing a new OpenAI feature for developers on Azure  | Microsoft Azure Blog](https://azure.microsoft.com/en-us/blog/announcing-a-new-openai-feature-for-developers-on-azure/)
[Validating OpenAPI and JSON Schema (json-schema.org)](https://json-schema.org/blog/posts/validating-openapi-and-json-schema#light-scheme-icon)