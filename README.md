# Concourse app store review resource

Checks for new app store reviews in the apple app store


## Resource Configuration

```yaml
resource_types:
- name: app_review
  type: docker-image
  source:
    repository: arwineap/concourse-appstore-review-resource
    tag: latest
```

## Resource Configuration

* app_id

### Example
```yaml
- name: facebook_app
  type: app_review
  source:
    app_id: '284882215'
```


## Behavior

### `check`: Check for new apple app store review
Gets a new apple app store review, drops a json, and a msg (formatted for slack)


#### Examples
```yaml
jobs:
- name: app_reviews
  plan:
  - get: facebook_app
    trigger: true
  - put: slack
    params:
      channel: '#general'
      text_file: facebook_app/slack.msg
resource_types:
- name: app_review
  type: docker-image
  source:
    repository: arwineap/concourse-appstore-review-resource
    tag: latest
resources:
- name: facebook_app
  type: app_review
  source:
    app_id: '284882215'

```


