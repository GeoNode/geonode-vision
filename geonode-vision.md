# Draft GeoNode 3.0 Vision Statement

This is a draft vision statement for GeoNode 3.0 provided for community discussion and collaboration.  It is purely for guiding discusion and not fixed.  The vision consists of the following reinforcing principles:

- [Django](#django)
- [Minimal core](#minimal-core)
- [Behavior Driven Development](#behavior-driven-development)
- [Fresh Start](#fresh-start)
- [Web UI Framework Agnostic](#web-ui-framework-agnostic)
- [API First & API Gateway](#api-first--api-gateway)
- [Support for multiple data providers](#support-for-multiple-data-providers)

Essentially:

- GeoNode 1 was a proof of concept.
- GeoNode 2 is a working product.
- GeoNode 3 is a scalable product.

# Django

GeoNode 3.0, as the previous versions, will continue to be built on [Django](https://www.djangoproject.com/).  However, it's usage of Django will adapt to the modern software environment.  The community-supported GeoNode version will continue to use [PostGIS](http://postgis.net/) as the recommended database for Django.

# Minimal Core

The future **core** Django python library of GeoNode should be minimal and consist of only support for database models and API views.  Front-end code, assets, etc. should be independent of the core Django application codebase.  This core will include at least layers, maps, and documents.

# Behavior Driven Development

GeoNode 3.0 should adopt a [behavior driven development](https://en.wikipedia.org/wiki/Behavior_Driven_Development) approach.  All features are described as behavioral tests using Python [Behave](http://pythonhosted.org/behave/index.html) or similar library.  These behaviors, all together, describe the entire API surface.

# Fresh Start

GeoNode 3.0 codebase should be it's own separate repo.  Code, including core database models, will be ported over to the new codebase as needed.  Fresh CSW, security, etc. sub-systems will be incorporated over time.

# Web UI Framework Agnostic

GeoNode 3.0 should support [Angular](https://angular.io/), [React](https://facebook.github.io/react/), [Preact](https://preactjs.com/), or [Vue.js](https://vuejs.org/) by being web UI agnostic.  All interaction with the GeoNode app server should take place via well documented (REST) APIs.  Common front-end components should be managed within their own relevant ecosystem (Angular Modules, etc.) rather than as Django apps.  They'll be no community support for instances based on Django html templates.

**Rationale**

When Geonode 1 was initially developed, the web was a very different place.  Modern web frameworks like [Angular](https://angular.io/) and [React](https://facebook.github.io/react/) did not exist.  For GeoNode 1, the benefit of using shared Django html templates made great sense as developing and maintaining web pages had a high cost.  Shared templates were necessary to deliver a turnkey solution.  GeoNode 2 reduced the cost of deployment even further by switching to using [Bootstrap](http://getbootstrap.com/).  HTML templates also allowed customization by organizations.

Today, modern websites are built on one of the common web UI frameworks and [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) web APIs rather than server rendered html pages.  Additionally, organizations usually want to have a unifying "brand" and user experience that encompasses their web presence, rather than just a logo.  By being web UI framework agnostic, GeoNode can support a wider variety of user experiences and be tailored to fit an instituion's needs.

# API First & API Gateway

The **core** codebase will take an API-first approach likely using [Django REST Framework](http://www.django-rest-framework.org/) (DRF) w/ support for [Swagger UI](https://swagger.io/swagger-ui/).

Since GeoNode 3.0 will be web UI agnostic, a common gateway will be used to interact with the GeoNode backend (based on the API first approach) rather than APIs for specific web UI frameworks.

# Support for Multiple Data Providers

GeoNode should be built to support multiple data providers, including:
- [GeoServer](http://geoserver.org/),
- [QGIS Server](http://docs.qgis.org/1.8/en/docs/user_manual/working_with_ogc/ogc_server_support.html),
- [Tegola](http://tegola.io/),
- [Solr](https://lucene.apache.org/solr/),
- [Elasticsearch](https://www.elastic.co/products/elasticsearch)/[ElasticGeo](https://github.com/ngageoint/elasticgeo), and
- [GeoMesa](http://www.geomesa.org/).

**Implementation**

Django's [PostgreSQL contrib app](https://docs.djangoproject.com/en/1.11/ref/contrib/postgres/fields/) may provide flexibility we can leverage to avoid overly complicated database models while still covering multiple data providers.  For example, we could use a single [HstoreField](https://docs.djangoproject.com/en/1.11/ref/contrib/postgres/fields/#django.contrib.postgres.fields.HStoreField) to store a dict of backend authentication parameters.
