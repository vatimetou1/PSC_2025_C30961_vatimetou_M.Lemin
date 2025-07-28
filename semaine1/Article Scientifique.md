📄 Article traité :
"UI2Code: Bridging the Gap Between UI Design and Code Generation Using Vision-Language Models"
(Publié dans ACM Transactions on Software Engineering and Methodology, avril 2024)

🎯 Problématique
La transformation d’une maquette UI en code reste un goulot d’étranglement dans le développement logiciel. Malgré les avancées, les systèmes existants souffrent d’un manque de compréhension sémantique globale de l’interface utilisateur, ce qui limite la qualité et la flexibilité du code généré. La plupart des systèmes se basent uniquement sur la détection visuelle sans tirer parti du contexte linguistique souvent présent dans les designs.

💡 Approche proposée
Cet article propose UI2Code, un modèle hybride combinant la vision par ordinateur et des modèles de langage visuels (comme CLIP, BLIP ou Flamingo) pour une meilleure compréhension contextuelle des maquettes UI.

L’approche suit trois étapes :

Encodage visuel de la maquette via un backbone CNN.

Encodage sémantique des textes et composants UI avec un modèle Vision-Language.

Décodage structuré en code XML/HTML à l’aide d’un décodeur de type Transformer.

UI2Code vise à générer un code plus fidèle sémantiquement et visuellement à la maquette d’origine.

⚙️ Technologies utilisées
CLIP (OpenAI) ou BLIP pour relier la vision et le langage.

CNN (ResNet / EfficientNet) pour l’extraction visuelle.

Transformers pour la génération de code séquentiel.

OCR avancé pour interpréter les textes dans les images UI.

Vision Transformer (ViT) pour une compréhension contextuelle globale.

Datasets utilisés : Pix2Code, Rico, et un nouveau dataset UI-VLM introduit par les auteurs.

🔭 Perspectives de recherche
L’article ouvre plusieurs pistes intéressantes :

Alignement sémantique : améliorer la correspondance entre les textes détectés et les composants UI associés.

Multimodalité : intégrer des descriptions vocales ou textuelles (par ex. Figma comments) pour renforcer la compréhension.

Cross-platform Code Generation : générer automatiquement du code pour plusieurs plateformes (Web, Android, iOS) à partir d’une seule maquette.

Évaluation plus réaliste : développer des benchmarks basés sur des projets industriels réels plutôt que sur des maquettes synthétiques.

Fine-tuning des modèles VLM pour des interfaces complexes (dashboards, jeux, etc.)