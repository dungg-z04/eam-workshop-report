---
title: "Event 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---


# BÃ i thu hoáº¡ch â€œGenAI-powered App-DB Modernization workshopâ€

### Má»¥c ÄÃ­ch Cá»§a Sá»± Kiá»‡n

- Chia sáº» best practices trong thiáº¿t káº¿ á»©ng dá»¥ng hiá»‡n Ä‘áº¡i
- Giá»›i thiá»‡u phÆ°Æ¡ng phÃ¡p DDD vÃ  event-driven architecture
- HÆ°á»›ng dáº«n lá»±a chá»n compute services phÃ¹ há»£p
- Giá»›i thiá»‡u cÃ´ng cá»¥ AI há»— trá»£ development lifecycle

### Danh SÃ¡ch Diá»…n Giáº£

- **Jignesh Shah** - Director, Open Source Databases
- **Erica Liu** - Sr. GTM Specialist, AppMod
- **Fabrianne Effendi** - Assc. Specialist SA, Serverless Amazon Web Services

### Ná»™i Dung Ná»•i Báº­t

#### ÄÆ°a ra cÃ¡c áº£nh hÆ°á»Ÿng tiÃªu cá»±c cá»§a kiáº¿n trÃºc á»©ng dá»¥ng cÅ©

- Thá»i gian release sáº£n pháº©m lÃ¢u â†’ Máº¥t doanh thu/bá» lá»¡ cÆ¡ há»™i
- Hoáº¡t Ä‘á»™ng kÃ©m hiá»‡u quáº£ â†’ Máº¥t nÄƒng suáº¥t, tá»‘n kÃ©m chi phÃ­
- KhÃ´ng tuÃ¢n thá»§ cÃ¡c quy Ä‘á»‹nh vá» báº£o máº­t â†’ Máº¥t an ninh, uy tÃ­n

#### Chuyá»ƒn Ä‘á»•i sang kiáº¿n trÃºc á»©ng dá»¥ng má»›i - Microservice Architecture

Chuyá»ƒn Ä‘á»•i thÃ nh há»‡ thá»‘ng modular â€“ tá»«ng chá»©c nÄƒng lÃ  má»™t **dá»‹ch vá»¥ Ä‘á»™c láº­p** giao tiáº¿p vá»›i nhau qua **sá»± kiá»‡n** vá»›i 3 trá»¥ cá»™t cá»‘t lÃµi:

- **Queue Management**: Xá»­ lÃ½ tÃ¡c vá»¥ báº¥t Ä‘á»“ng bá»™
- **Caching Strategy:** Tá»‘i Æ°u performance
- **Message Handling:** Giao tiáº¿p linh hoáº¡t giá»¯a services

#### Domain-Driven Design (DDD)

- **PhÆ°Æ¡ng phÃ¡p 4 bÆ°á»›c**: XÃ¡c Ä‘á»‹nh domain events â†’ sáº¯p xáº¿p timeline â†’ identify actors â†’ xÃ¡c Ä‘á»‹nh bounded contexts
- **Case study bookstore**: Minh há»a cÃ¡ch Ã¡p dá»¥ng DDD thá»±c táº¿
- **Context mapping**: 7 patterns tÃ­ch há»£p bounded contexts

#### Event-Driven Architecture

- **3 patterns tÃ­ch há»£p**: Publish/Subscribe, Point-to-point, Streaming
- **Lá»£i Ã­ch**: Loose coupling, scalability, resilience
- **So sÃ¡nh sync vs async**: Hiá»ƒu rÃµ trade-offs (sá»± Ä‘Ã¡nh Ä‘á»•i)

#### Compute Evolution

- **Shared Responsibility Model**: Tá»« EC2 â†’ ECS â†’ Fargate â†’ Lambda
- **Serverless benefits**: No server management, auto-scaling, pay-for-value
- **Functions vs Containers**: Criteria lá»±a chá»n phÃ¹ há»£p

#### Amazon Q Developer

- **SDLC automation**: Tá»« planning Ä‘áº¿n maintenance
- **Code transformation**: Java upgrade, .NET modernization
- **AWS Transform agents**: VMware, Mainframe, .NET migration

### Nhá»¯ng GÃ¬ Há»c ÄÆ°á»£c

#### TÆ° Duy Thiáº¿t Káº¿

- **Business-first approach**: LuÃ´n báº¯t Ä‘áº§u tá»« business domain, khÃ´ng pháº£i technology
- **Ubiquitous language**: Importance cá»§a common vocabulary giá»¯a business vÃ  tech teams
- **Bounded contexts**: CÃ¡ch identify vÃ  manage complexity trong large systems

#### Kiáº¿n TrÃºc Ká»¹ Thuáº­t

- **Event storming technique**: PhÆ°Æ¡ng phÃ¡p thá»±c táº¿ Ä‘á»ƒ mÃ´ hÃ¬nh hÃ³a quy trÃ¬nh kinh doanh
- Sá»­ dá»¥ng **Event-driven communication** thay vÃ¬ synchronous calls
- **Integration patterns**: Hiá»ƒu khi nÃ o dÃ¹ng sync, async, pub/sub, streaming
- **Compute spectrum**: Criteria chá»n tá»« VM â†’ containers â†’ serverless

#### Chiáº¿n LÆ°á»£c Hiá»‡n Äáº¡i HÃ³a

- **Phased approach**: KhÃ´ng rush, pháº£i cÃ³ roadmap rÃµ rÃ ng
- **7Rs framework**: Nhiá»u con Ä‘Æ°á»ng khÃ¡c nhau tÃ¹y thuá»™c vÃ o Ä‘áº·c Ä‘iá»ƒm cá»§a má»—i á»©ng dá»¥ng
- **ROI measurement**: Cost reduction + business agility

### á»¨ng Dá»¥ng VÃ o CÃ´ng Viá»‡c

- **Ãp dá»¥ng DDD** cho project hiá»‡n táº¡i: Event storming sessions vá»›i business team
- **Refactor microservices**: Sá»­ dá»¥ng bounded contexts Ä‘á»ƒ identify service boundaries
- **Implement event-driven patterns**: Thay tháº¿ má»™t sá»‘ sync calls báº±ng async messaging
- **Serverless adoption**: Pilot AWS Lambda cho má»™t sá»‘ use cases phÃ¹ há»£p
- **Try Amazon Q Developer**: Integrate vÃ o development workflow Ä‘á»ƒ boost productivity

### Tráº£i nghiá»‡m trong event

Tham gia workshop **â€œGenAI-powered App-DB Modernizationâ€** lÃ  má»™t tráº£i nghiá»‡m ráº¥t bá»• Ã­ch, giÃºp tÃ´i cÃ³ cÃ¡i nhÃ¬n toÃ n diá»‡n vá» cÃ¡ch hiá»‡n Ä‘áº¡i hÃ³a á»©ng dá»¥ng vÃ  cÆ¡ sá»Ÿ dá»¯ liá»‡u báº±ng cÃ¡c phÆ°Æ¡ng phÃ¡p vÃ  cÃ´ng cá»¥ hiá»‡n Ä‘áº¡i. Má»™t sá»‘ tráº£i nghiá»‡m ná»•i báº­t:

#### Há»c há»i tá»« cÃ¡c diá»…n giáº£ cÃ³ chuyÃªn mÃ´n cao
- CÃ¡c diá»…n giáº£ Ä‘áº¿n tá»« AWS vÃ  cÃ¡c tá»• chá»©c cÃ´ng nghá»‡ lá»›n Ä‘Ã£ chia sáº» **best practices** trong thiáº¿t káº¿ á»©ng dá»¥ng hiá»‡n Ä‘áº¡i.
- Qua cÃ¡c case study thá»±c táº¿, tÃ´i hiá»ƒu rÃµ hÆ¡n cÃ¡ch Ã¡p dá»¥ng **Domain-Driven Design (DDD)** vÃ  **Event-Driven Architecture** vÃ o cÃ¡c project lá»›n.

#### Tráº£i nghiá»‡m ká»¹ thuáº­t thá»±c táº¿
- Tham gia cÃ¡c phiÃªn trÃ¬nh bÃ y vá» **event storming** giÃºp tÃ´i hÃ¬nh dung cÃ¡ch **mÃ´ hÃ¬nh hÃ³a quy trÃ¬nh kinh doanh** thÃ nh cÃ¡c domain events.
- Há»c cÃ¡ch **phÃ¢n tÃ¡ch microservices** vÃ  xÃ¡c Ä‘á»‹nh **bounded contexts** Ä‘á»ƒ quáº£n lÃ½ sá»± phá»©c táº¡p cá»§a há»‡ thá»‘ng lá»›n.
- Hiá»ƒu rÃµ trade-offs giá»¯a **synchronous vÃ  asynchronous communication** cÅ©ng nhÆ° cÃ¡c pattern tÃ­ch há»£p nhÆ° **pub/sub, point-to-point, streaming**.

#### á»¨ng dá»¥ng cÃ´ng cá»¥ hiá»‡n Ä‘áº¡i
- Trá»±c tiáº¿p tÃ¬m hiá»ƒu vá» **Amazon Q Developer**, cÃ´ng cá»¥ AI há»— trá»£ SDLC tá»« láº­p káº¿ hoáº¡ch Ä‘áº¿n maintenance.
- Há»c cÃ¡ch **tá»± Ä‘á»™ng hÃ³a code transformation** vÃ  pilot serverless vá»›i **AWS Lambda**, tá»« Ä‘Ã³ nÃ¢ng cao nÄƒng suáº¥t phÃ¡t triá»ƒn.

#### Káº¿t ná»‘i vÃ  trao Ä‘á»•i
- Workshop táº¡o cÆ¡ há»™i trao Ä‘á»•i trá»±c tiáº¿p vá»›i cÃ¡c chuyÃªn gia, Ä‘á»“ng nghiá»‡p vÃ  team business, giÃºp **nÃ¢ng cao ngÃ´n ngá»¯ chung (ubiquitous language)** giá»¯a business vÃ  tech.
- Qua cÃ¡c vÃ­ dá»¥ thá»±c táº¿, tÃ´i nháº­n ra táº§m quan trá»ng cá»§a **business-first approach**, luÃ´n báº¯t Ä‘áº§u tá»« nhu cáº§u kinh doanh thay vÃ¬ chá»‰ táº­p trung vÃ o cÃ´ng nghá»‡.

#### BÃ i há»c rÃºt ra
- Viá»‡c Ã¡p dá»¥ng DDD vÃ  event-driven patterns giÃºp giáº£m **coupling**, tÄƒng **scalability** vÃ  **resilience** cho há»‡ thá»‘ng.
- Chiáº¿n lÆ°á»£c hiá»‡n Ä‘áº¡i hÃ³a cáº§n **phased approach** vÃ  Ä‘o lÆ°á»ng **ROI**, khÃ´ng nÃªn vá»™i vÃ ng chuyá»ƒn Ä‘á»•i toÃ n bá»™ há»‡ thá»‘ng.
- CÃ¡c cÃ´ng cá»¥ AI nhÆ° Amazon Q Developer cÃ³ thá»ƒ **boost productivity** náº¿u Ä‘Æ°á»£c tÃ­ch há»£p vÃ o workflow phÃ¡t triá»ƒn hiá»‡n táº¡i.

#### Má»™t sá»‘ hÃ¬nh áº£nh khi tham gia sá»± kiá»‡n
* ThÃªm cÃ¡c hÃ¬nh áº£nh cá»§a cÃ¡c báº¡n táº¡i Ä‘Ã¢y
> Tá»•ng thá»ƒ, sá»± kiá»‡n khÃ´ng chá»‰ cung cáº¥p kiáº¿n thá»©c ká»¹ thuáº­t mÃ  cÃ²n giÃºp tÃ´i thay Ä‘á»•i cÃ¡ch tÆ° duy vá» thiáº¿t káº¿ á»©ng dá»¥ng, hiá»‡n Ä‘áº¡i hÃ³a há»‡ thá»‘ng vÃ  phá»‘i há»£p hiá»‡u quáº£ hÆ¡n giá»¯a cÃ¡c team.
