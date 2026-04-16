---
theme: seriph
title: "Nous voulons toujours des chevaux plus rapides"
titleTemplate: "%s — Django Meetup"
info: |
  Inspiré de l'article "Rich Text Fields and Faster Horses"
  par Matthew Westcott (Wagtail Tech Lead, 2015)
author: "Darko Stankovski"
keywords: django,wagtail,cms,streamfield,rich-text
class: text-center
highlighter: shiki
lineNumbers: true
drawings:
  persist: false
transition: slide-left
mdc: true
---

<div class="absolute inset-0 bg-white" />

<div class="flex flex-col items-center justify-center h-full gap-6 relative z-10">

<div class="text-6xl font-bold leading-tight max-w-3xl bg-gradient-to-r from-green-700 via-emerald-500 to-teal-400 bg-clip-text text-transparent">
  Nous voulons toujours des chevaux plus rapides
</div>

<div class="text-xl text-gray-500 mt-2">
  Les éditeurs WYSIWYG et le contenu structuré en Django/Wagtail
</div>

<div class="mt-8 flex items-center gap-3 text-gray-400 text-sm">
  <span class="px-3 py-1 rounded-full border border-gray-300">Paris Django Meetup</span>
  <span>·</span>
  <span>2026</span>
</div>

</div>

---
layout: image-right
image: /images/darko-stankovski.jpeg
---

# Qui suis-je ?

**Darko Stankovski**

- Développeur Python / Django depuis… longtemps
- Indépendant
- Derniers intérêts : Django/Wagtail

<br>

**Contact**
- GitHub: `@darko-itpro`
- LinkedIn: darko-stankovski

**Blog**
- taverneinvisible.net

---
layout: image
image: /images/horse-faster.jpg
class: text-center
---

# "Si j'avais demandé aux gens ce qu'ils voulaient..."

<div class="absolute bottom-10 left-0 right-0 text-center bg-black/60 py-4 px-8">

## "...ils auraient demandé des chevaux plus rapides."

_— Henry Ford (attribué)_

</div>

---
layout: two-cols
---

# L'article source

::left::

**"Rich Text Fields and Faster Horses"**

Par **Matthew Westcott**  
Wagtail Tech Lead — Torchbox, 2015

<br>

- Article fondateur sur la philosophie Wagtail
- Articule le passage du WYSIWYG au contenu structuré
- Toujours pertinent 10 ans plus tard

<br>

**Lien vers l'article :**  
[torchbox.com — Rich Text Fields and Faster Horses](https://torchbox.com/wagtail-cms-services/blog/rich-text-fields-and-faster-horses/)

::right::

<div class="flex flex-col items-center justify-center h-full gap-4">

<img src="/images/wagtail-logo.png" alt="Logo Wagtail" class="w-32" />

</div>

---
layout: center
class: text-center
transition: fade
---

# Une question pour commencer

<br>

## Django est-il un CMS ?

---
layout: center
class: text-center
---

# Une question pour commencer

<br>

## Non, Django n'est pas un CMS !

<br />

<v-click>

* Pas de gestion d'images, documents

</v-click>
<v-click>

* Pas de gestion native de workflows

</v-click>
<v-click>

* Est-il destiné à des éditeurs sans connaissance technique ?

</v-click>

---
layout: section
---

# Le problème

## Nous n'avons pas évolué depuis l'utilisation des chevaux

---
title: Illustration machine à écrire
layout: center
class: text-center
---

<img src="/images/Underwood-machine-ecrire.jpg" alt="Machine à écrire Underwood" class="h-[60vh] w-auto mx-auto object-contain" />

<!--
L'informatique grand public, c'est la bureautique avec historiquement la sortie papier
-->

---
layout: default
---

# Nous avons toujours une vision _papier_ du contenu

 * Historiquement Word (OpenOffice…) et <span>L<sup class="text-[0.7em] relative top-[-0.15em]">A</sup>T<sub class="text-[0.7em] relative top-[0.15em]">E</sub>X</span>
 * Depuis, Google Docs…

<v-click>

 * Et le HTML…

</v-click>
 <v-click>

 * Markdown et RST suivent la structure HTML
 * MkDocs ou Quarto suivent la logique de <span>L<sup class="text-[0.7em] relative top-[-0.15em]">A</sup>T<sub class="text-[0.7em] relative top-[0.15em]">E</sub>X</span>

</v-click>

---
title: Illustration champ texte brut
layout: center
class: text-center
transition: fade
---

<img src="/images/blog_post_text_form.png" alt="Formulaire post blog" class="h-[60vh] w-auto mx-auto object-contain" />

<!--
Les formulaires de base d'un blog Django
-->

---
title: Illustration champ texte avec Prose
layout: center
class: text-center
---

<img src="/images/blog_post_prose_form.png" alt="Formulaire post blog avec Prose" class="h-[60vh] w-auto mx-auto object-contain" />

<!--
Les formulaires de base d'un blog Django enrichi avec Prose
-->

---
title: Illustration RichTextField
layout: center
class: text-center
---

<img src="/images/blog_post_wagtail_richtext_form_1.png" alt="Formulaire post blog avec RichTextField" class="h-[60vh] w-auto mx-auto object-contain" />

<!--
Les formulaires Richtextfield Wagtail 
-->

---
title: Illustration image et légende
layout: center
class: text-center
---

<img src="/images/blog_page_caption_image.png" alt="Contenu avec image et légende" class="h-[60vh] w-auto mx-auto object-contain" />

---
title: Illustration galerie d'images
layout: center
class: text-center
---

<img src="/images/blog_page_gallery.png" alt="Contenu avec galerie d'images" class="h-[60vh] w-auto mx-auto object-contain" />

---
layout: section
---

# Le problème

## Pourquoi les éditeurs WYSIWYG nous font défaut

---
layout: center
class: text-center
---

# Le vrai problème : la confusion fond / forme

<div class="grid grid-cols-2 gap-8 mt-8 text-left">

<div class="bg-red-50 rounded-lg p-6 border border-red-200">

**Ce que l'éditeur capture**

```html
<h2 style="color: #333; font-size: 1.5em">
  Jeudi 16 avril 2026
</h2>
```

Mise en forme visuelle.  
Aucun sens sémantique.

</div>

<div class="bg-green-50 rounded-lg p-6 border border-green-200">

**Ce que le système devrait capturer**

```python
event.date = date(2026, 4, 16)
event.title = "Django Meetup"
```

Donnée structurée.  
Sens explicite.  
Réutilisable.

</div>

</div>

---
layout: center
---

# Le problème du contenu embarqué

Un éditeur vous permet de coller du HTML Google Maps.

**Ce qui est stocké :**

```html
<iframe src="https://maps.google.com/...
  &q=SW1A+1AA&..."></iframe>
```

**Ce qui est perdu :**

- Le vrai code postal : `SW1A 1AA`
- La possibilité de réafficher sur une autre carte
- La possibilité de migrer vers OpenStreetMap
- Toute extraction de données future

<br>

_Le sens sémantique est noyé dans la présentation._

<!--
Exemple concret de l'article original. Très parlant pour une audience technique.
Insister sur l'irréversibilité : une fois stocké comme blob HTML,
on ne peut plus jamais retrouver la donnée d'origine proprement.
Remplacer /images/google-maps-html.png par une capture illustrant le problème.
-->

---
layout: section
---

# La solution

## Penser en blocs, pas en paragraphes

<!--
Transition vers la deuxième partie. Ton plus optimiste.
-->

---
layout: center
image: /images/streamfield-ui.png
---

# StreamField : le contenu comme blocs typés

Au lieu d'un grand champ texte, la page est composée de **blocs typés** :

- `ParagraphBlock` — texte enrichi limité
- `ImageBlock` — image avec légende, alt text et auteur
- `MapBlock` — champ code postal → carte générée
- `CodeBlock` — code avec coloration syntaxique
- `QuoteBlock` — citation avec attribution

<br>

Chaque bloc a **l'interface de saisie adaptée à sa nature**.

<!--
C'est la révélation de la présentation. StreamField existe depuis Wagtail 1.0 (2015).
Montrer une démo live du chooser de blocs si possible.
Remplacer /images/streamfield-ui.png par une capture de l'interface StreamField.
-->

---
layout: default
---

# Exemple de bloc pour une image et une citation

```python
class ImageBlock(StructBlock):
    image = ImageChooserBlock()
    caption = CharBlock(required=False)
    author = CharBlock(required=False)

    class Meta:
        icon = 'image'
        template = 'components/streamfield/blocks/image_block.html'

class QuoteBlock(StructBlock):
    text = RichTextBlock(features=['bold', 'italic', 'link', 'ol', 'ul'])
    attribution = CharBlock(required=False,
                            blank=True,
                            help_text="e.g. John Doe or J. Doe")

    class Meta:
        icon = 'quote'
        template = 'components/streamfield/blocks/quote.html'

```

---
layout: default
---

# Exemple de bloc pour une image et une citation

```python
class BaseBlogBlock(StreamBlock):
    paragraph = RichTextBlock(features=["h2", "h3", "bold", "italic", 
                                        "link", "ol", "ul", "document-link", "code"],
                              icon="pilcrow")
    image = ImageBlock()
    quote = QuoteBlock()
    embed = EmbedBlock(max_width=800, max_height=400)
    code = CodeBlock(label="Code")

```

<br />

```python
class ArticlePage(BaseArticlePage):
    body = StreamField(BaseBlogBlock,
                       verbose_name="Post body",
                       blank=True,
                       use_json_field=True,
                       )
    content_panels = BaseArticlePage.content_panels + [
        FieldPanel("body"),
    ]
```

---
title: Illustration formulaire
layout: center
class: text-center
transition: fade
---

<img src="/images/blocks_add_block.png" alt="Formulaire ajout élément" class="h-[60vh] w-auto mx-auto object-contain" />

---
title: Illustration formulaire
layout: center
class: text-center
transition: fade
---

<img src="/images/blocks_image_block.png" alt="Formulaire image" class="h-[60vh] w-auto mx-auto object-contain" />

---
layout: center
---

# Les bénéfices du contenu structuré

**Pour les éditeurs**
- Interface adaptée à chaque type de contenu
- Impossibilité de faire des erreurs de mise en forme
- Réordonnancement via le formulaire

**Pour les développeurs**
- Données interrogeables et migrables
- API propre (JSON structuré)
- Rendu personnalisable sans toucher au contenu

**Pour le site**
- Cohérence visuelle automatique
- SEO amélioré (données structurées)
- Futur-proof : changer le rendu sans changer les données

<br>

> Le contenu sémantique **survit** aux refontes graphiques.

---
layout: center
class: text-center
---

# En résumé

<div class="grid grid-cols-3 gap-6 mt-8">

<div class="bg-red-50 rounded-xl p-6 border border-red-200">

**Cheval plus rapide**

Ajouter des boutons  
à l'éditeur WYSIWYG

_Plus de contrôle...  
moins de sens_

</div>

<div class="text-4xl flex items-center justify-center">→</div>

<div class="bg-green-50 rounded-xl p-6 border border-green-200">

**L'innovation**

Blocs sémantiques  
avec éditeurs dédiés

_Moins de liberté...  
plus de valeur_

</div>

</div>

<br>

> "Capturer **ce que le contenu signifie**,  
> pas seulement comment il est mis en forme."

---
layout: end
class: text-center
---

# Merci !

**Questions ?**

<div class="pt-8 text-gray-500">

Article original : [torchbox.com — Rich Text Fields and Faster Horses](https://torchbox.com/wagtail-cms-services/blog/rich-text-fields-and-faster-horses/)

Documentation Wagtail StreamField : [docs.wagtail.org/en/stable/topics/streamfield.html](https://docs.wagtail.org/en/stable/topics/streamfield.html)

</div>

<div class="pt-4 text-sm text-gray-400">

Darko Stankovski · Paris Django Meetup · 2026

</div>
