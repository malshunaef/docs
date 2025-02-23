---
title: Tipos de evento de GitHub
intro: 'Para la API de Eventos de {% data variables.product.prodname_dotcom %}, aprende acerca de cada tipo de evento, la acción que los desencadena en {% data variables.product.prodname_dotcom %}, y las propiedades exclusivas de cada evento.'
redirect_from:
  - /v3/activity/event_types
  - /developers/webhooks-and-events/github-event-types
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Events
---

La API de eventos puede devolver diferentes tipos de ventos que se activan de acuerdo a la actividad en GitHub. Cada respuesta de evento contiene propiedades compartidas, pero tiene un objeto único de `payload` que se determina por su tipo de evento. Las [propiedades comunes del objeto de los eventos](#event-object-common-properties) describen aquellas propiedades que comparten todos los eventos, y cada tipo de evento describe las propiedades de la `payload` que son exclusivas para éste.

{% ifversion fpt or ghec %}

{% endif %}

## Propiedades comunes del objeto de los eventos

Los objetos de los eventos que se devuelven de las terminales de la API de Eventos tienen la misma estructura.

| Nombre del atributo de la API del Evento | Descripción                                                                                                                                                                                               |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                     | Identificador único para el evento.                                                                                                                                                                       |
| `type`                                   | El tipo de evento. Los eventos utilizan PascalCase para el nombre.                                                                                                                                        |
| `actor (actor)`                          | El usuario que activó el evento.                                                                                                                                                                          |
| `actor.id`                               | El identificador único para el actor.                                                                                                                                                                     |
| `actor.login`                            | El nombre de usuario para el actor.                                                                                                                                                                       |
| `actor.display_login`                    | El formato de visualización específico para el nombre de usuario.                                                                                                                                         |
| `actor.gravatar_id`                      | El identificador único del perfil de Gravatar para el actor.                                                                                                                                              |
| `actor.url`                              | La URL de la API de REST que se utiliza para recuperar el objeto del usuario, el cual incluye información adicional del usuario.                                                                          |
| `actor.avatar_url`                       | La URL de la imagen de perfil del actor.                                                                                                                                                                  |
| `repo`                                   | El objeto del repositorio en donde ocurrió el evento.                                                                                                                                                     |
| `repo.id`                                | El identificador único del repositorio.                                                                                                                                                                   |
| `repo.name`                              | El nombre del repositorio, el cual incluye también al nombre del propietario. Por ejemplo, `octocat/hello-world` es el nombre del repositorio `hello-world` que pertenece a la cuenta personal `octocat`. |
| `repo.url`                               | La URL de la API de REST que se utiliza para recuperar el objeto del repositorio, el cual incluye información adicional sobre dicho repositorio.                                                          |
| `payload`                                | El objeto de la carga útil del evento que es exclusivo para el tipo de evento. En el siguiente ejemplo puedes ver el tipo de evento para el objeto de `payload` de la API de eventos.                     |
| `public`                                 | Whether the event is visible to all users.                                                                                                                                                                |
| `created_at (creado en)`                 | The date and time when the event was triggered. It is formatted according to ISO 8601.                                                                                                                    |
| `org`                                    | The organization that was chosen by the actor to perform action that triggers the event.<br />_The property appears in the event object only if it is applicable._                                |
| `org.id`                                 | The unique identifier for the organization.                                                                                                                                                               |
| `org.login`                              | The name of the organization.                                                                                                                                                                             |
| `org.gravatar_id`                        | The unique identifier of the Gravatar profile for the organization.                                                                                                                                       |
| `org.url`                                | The REST API URL used to retrieve the organization object, which includes additional organization information.                                                                                            |
| `org.avatar_url`                         | The URL of the organization's profile image.                                                                                                                                                              |

### Ejemplo con el objeto de evento WatchEvent

Este ejemplo te muestra el formato de la respuesta de [WatchEvent](#watchevent) cuando utilizas la [API de Eventos](/rest/reference/activity#events).

```
HTTP/2 200
Link: <https://api.github.com/resource?page=2>; rel="next",
      <https://api.github.com/resource?page=5>; rel="last"
```
```json
[
  {
    "type": "WatchEvent",
    "public": false,
    "payload": {
    },
    "repo": {
      "id": 3,
      "name": "octocat/Hello-World",
      "url": "https://api.github.com/repos/octocat/Hello-World"
    },
    "actor": {
      "id": 1,
      "login": "octocat",
      "gravatar_id": "",
      "avatar_url": "https://github.com/images/error/octocat_happy.gif",
      "url": "https://api.github.com/users/octocat"
    },
    "org": {
      "id": 1,
      "login": "github",
      "gravatar_id": "",
      "url": "https://api.github.com/orgs/github",
      "avatar_url": "https://github.com/images/error/octocat_happy.gif"
    },
    "created_at": "2011-09-06T17:26:27Z",
    "id": "12345"
  }
]
```

## CommitCommentEvent

{% data reusables.webhooks.commit_comment_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.commit_comment_properties %}

## CreateEvent

{% data reusables.webhooks.create_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.create_properties %}

## DeleteEvent

{% data reusables.webhooks.delete_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.delete_properties %}

## ForkEvent

{% data reusables.webhooks.fork_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.fork_properties %}

## GollumEvent

{% data reusables.webhooks.gollum_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.gollum_properties %}

## IssueCommentEvent

{% data reusables.webhooks.issue_comment_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.issue_comment_webhook_properties %}
{% data reusables.webhooks.issue_comment_properties %}

## IssuesEvent

{% data reusables.webhooks.issues_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.issue_event_api_properties %}
{% data reusables.webhooks.issue_properties %}

## MemberEvent

{% data reusables.webhooks.member_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.member_event_api_properties %}
{% data reusables.webhooks.member_properties %}

{% ifversion fpt or ghes or ghec %}
## PublicEvent

{% data reusables.webhooks.public_short_desc %}
### Objeto de `payload` del evento

Este evento devuelve un objeto de `payload` vacío.
{% endif %}
## PullRequestEvent

{% data reusables.webhooks.pull_request_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.pull_request_event_api_properties %}
{% data reusables.webhooks.pull_request_properties %}

## PullRequestReviewEvent

{% data reusables.webhooks.pull_request_review_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

| Clave                  | Tipo        | Descripción                                              |
| ---------------------- | ----------- | -------------------------------------------------------- |
| `Acción`               | `secuencia` | La acción que se realizó. Puede ser `created`.           |
| `solicitud_extracción` | `objeto`    | La solicitud de cambios a la cual pertenece la revisión. |
| `revisar`              | `objeto`    | La revisión que se afectó.                               |

## PullRequestReviewCommentEvent

{% data reusables.webhooks.pull_request_review_comment_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.pull_request_review_comment_event_api_properties %}
{% data reusables.webhooks.pull_request_review_comment_properties %}

## PullRequestReviewThreadEvent

{% data reusables.webhooks.pull_request_review_thread_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.pull_request_thread_properties %}

## PushEvent

{% data reusables.webhooks.push_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

| Clave                      | Tipo        | Descripción                                                                                                                                                                                                                                                                                                                                                                          |
| -------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `push_id`                  | `número`    | Identificador único para la carga.                                                                                                                                                                                                                                                                                                                                                   |
| `tamaño`                   | `número`    | La cantidad de confirmaciones de la carga.                                                                                                                                                                                                                                                                                                                                           |
| `distinct_size`            | `número`    | La cantidad de confimraciones distintas para la carga.                                                                                                                                                                                                                                                                                                                               |
| `ref`                      | `secuencia` | Toda la [`git ref`](/rest/reference/git#refs) que se cargó. Ejemplo: `refs/heads/main`.                                                                                                                                                                                                                                                                                              |
| `encabezado`               | `secuencia` | El SHA de la confirmación más reciente en `ref` después de la carga.                                                                                                                                                                                                                                                                                                                 |
| `before`                   | `secuencia` | El SHA de la confirmación más reciente en `ref` antes de la carga.                                                                                                                                                                                                                                                                                                                   |
| `commits`                  | `arreglo`   | Un conjunto de objetos de confirmación que describen las confirmaciones subidas. (El conjunto incluye un máximo de 20 confirmaciones. De ser encesario, puedes utilizar la [API de confirmaciones](/rest/reference/repos#commits) para recuperar confirmaciones adicionales. Este límite se aplica a los eventos cronológicos únicamente y no se aplica a las entregas de webhooks). |
| `commits[][sha]`           | `secuencia` | El SHA de la confirmación.                                                                                                                                                                                                                                                                                                                                                           |
| `commits[][message]`       | `secuencia` | El mensaje de la confirmación.                                                                                                                                                                                                                                                                                                                                                       |
| `commits[][author]`        | `objeto`    | El autor de git de la confirmación.                                                                                                                                                                                                                                                                                                                                                  |
| `commits[][author][name]`  | `secuencia` | El nombre del autor de git.                                                                                                                                                                                                                                                                                                                                                          |
| `commits[][author][email]` | `secuencia` | La dirección de correo electrónico del autor de git.                                                                                                                                                                                                                                                                                                                                 |
| `commits[][url]`           | `url`       | URL que apunta al recurso de la API de la confirmación.                                                                                                                                                                                                                                                                                                                              |
| `commits[][distinct]`      | `boolean`   | Si la confirmación es distinta de cualquier otra que se haya subido antes.                                                                                                                                                                                                                                                                                                           |

## ReleaseEvent

{% data reusables.webhooks.release_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.release_event_api_properties %}
{% data reusables.webhooks.release_properties %}

{% ifversion fpt or ghec %}
## SponsorshipEvent

{% data reusables.webhooks.sponsorship_short_desc %}

### Objeto de `payload` del evento

{% data reusables.webhooks.sponsorship_event_api_properties %}
{% data reusables.webhooks.sponsorship_properties %}
{% endif %}

## WatchEvent

{% data reusables.webhooks.watch_short_desc %}

{% data reusables.webhooks.events_api_payload %}

### Objeto de `payload` del evento

{% data reusables.webhooks.watch_properties %}
