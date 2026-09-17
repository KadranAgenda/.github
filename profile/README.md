 ## Dépôts                                                                                                                                                                      
                  
  ### [kadran](https://github.com/kadran/kadran) — Application web (Laravel)                                                                                                     
                  
  Le cœur du système. Expose une API REST consommée par le bot et les widgets Android.                                                                                           
                  
  **Endpoints principaux :**                                                                                                                                                     
                  
  | Route | Description |                                                                                                                                                        
  |---|---|       
  | `GET /api/ping` | Vérifie la disponibilité du serveur |                                                                                                                      
  | `GET /api/day` | Événements et tâches du jour |                                                                                                                              
  | `GET /api/week` | Vue hebdomadaire |                                                                                                                                         
  | `GET /api/upcoming` | Prochains événements (7 jours) |                                                                                                                       
  | `GET /api/tasks?filter=pending` | Tâches en attente |                                                                                                                        
  | `GET /api/widget-setup/exchange` | Échange un code QR en identifiants |                                                                                                      
                                                                                                                                                                                 
  **Auth :** `Authorization: Bearer <AGENDA_API_TOKEN>` + `X-Discord-Id` pour le cloisonnement par utilisateur.                                                                  
                                                                                                                                                                                 
  ---                                                                                                                                                                            
                  
  ### [kadranBot](https://github.com/kadran/kadranBot) — Bot Discord                                                                                                             
                  
  Bot Discord qui interroge l'API Kadran et répond aux commandes slash dans le serveur. Utilise le même jeton API partagé (`AGENDA_API_TOKEN`) que le widget.                    
                  
  ---                                                                                                                                                                            
                  
  ### [KadranWidget](https://github.com/kadran/KadranWidget) — Widget Android                                                                                                    
                  
  Application Android proposant six widgets d'écran d'accueil qui affichent l'agenda et les tâches en temps réel, sans ouvrir l'app.                                             
                  
  **Widgets disponibles :**                                                                                                                                                      
                  
  | Widget | Format | Contenu |                                                                                                                                                  
  |---|---|---|   
  | Kadran · Jour | 4×2 | Événements du jour + tâches en attente |                                                                                                               
  | Kadran · Semaine | 4×2 | Vue compacte de la semaine |                                                                                                                        
  | Kadran · Agenda semaine | 4×4 | Agenda scrollable sur 7 jours |                                                                                                              
  | Kadran · Agenda mini | 2×2 | Événements du jour |                                                                                                                            
  | Kadran · Tâches mini | 2×2 | Tâches en attente |                                                                                                                             
  | Kadran · Statut | 4×1 | État du serveur + dernière mise à jour |                                                                                                             
                                                                                                                                                                                 
  Rafraîchissement automatique toutes les 15 minutes via WorkManager, avec bouton de refresh sur chaque widget. Configuration par QR code généré depuis l'app web.               
                                                                                                                                                                                 
  ---                                                                                                                                                                            
                  
  ## Architecture

  Discord ──────► kadranBot ──────►┐                                                                                                                                             
                                    ├──► API Laravel (kadran)
  Android ──────► KadranWidget ───►┘         │                                                                                                                                   
                                              └──► Base de données                                                                                                               
                                                                                                                                                                                 
  ---                                                                                                                                                                            
                                                                                                                                                                                 
  ## Auth partagée                                                                                                                                                               
   
  Les trois composants utilisent le même mécanisme :                                                                                                                             
                  
  Authorization: Bearer AGENDA_API_TOKEN                                                                                                                                         
  X-Discord-Id: <id numérique Discord de l'utilisateur>
                                                                                                                                                                                 
  Le serveur résout l'utilisateur depuis le `X-Discord-Id` via `ResolveDiscordUser` — aucun compte supplémentaire à créer.
