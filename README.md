# TP – Clients synchrones RestTemplate vs Feign vs WebClient avec Eureka / Consul

## 1. Objectifs pédagogiques

À la fin de ce lab, l’étudiant sera capable de :

- Implémenter **deux microservices** communiquant de manière **synchrone**
- Configurer la **découverte de services** avec **Eureka** et/ou **Consul**
- Implémenter **3 clients HTTP** côté *Service Client* :
  - `RestTemplate`
  - `OpenFeign`
  - `WebClient`
- Réaliser des **tests de performance** (latence / débit) et collecter des métriques
- Tester la **résilience** de l’architecture :
  - panne du service Voiture
  - panne du service de discovery (Eureka/Consul)
  - analyse des résultats observés

---
<img width="1916" height="1017" alt="image" src="https://github.com/user-attachments/assets/0cc554a4-526b-4b00-999b-4d5be979d7ed" />


- **Java** 17+ (ou 11+)
- **Maven**
- Un IDE : IntelliJ IDEA / Eclipse / VS Code
- **Postman** ou `curl` pour tester les API
- **JMeter** (recommandé) pour les tests de charge
- (Optionnel) **Docker** + **Docker Compose**
- (Optionnel) **Prometheus** + **Grafana** pour les métriques
- **Eureka** ou **Consul** comme serveur de discovery (selon le scénario du lab)

---

## 3. Architecture cible

### Microservices

- **Service Voiture**
  - Expose une API pour récupérer les voitures d’un client
- **Service Client**
  - Consomme l’API du Service Voiture via :
    - `RestTemplate`
    - `Feign`
    - `WebClient`

### Discovery

- Utilisation de **Eureka** ou **Consul** pour :
  - l’enregistrement des services
  - la résolution de noms logiques (SERVICE-VOITURE, etc.)

### Flux principal

```text
Service Client
    ↓ (RestTemplate / Feign / WebClient)
Service Voiture
    ↓
Discovery (Eureka / Consul) pour la résolution de nom
