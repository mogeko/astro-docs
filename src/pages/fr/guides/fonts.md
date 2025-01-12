---
title: Utiliser des polices personalisées
description: Vous souhaitez ajouter des polices de caractères personnalisées à un site Astro ? Utilisez Google Fonts avec Fontsource ou ajoutez une police de votre choix.
layout: ~/layouts/MainLayout.astro
setup: |
    import PackageManagerTabs from '~/components/tabs/PackageManagerTabs.astro';
---

Astro prend en charge toutes les stratégies courantes pour ajouter des polices de caractères personnalisées à la conception de votre site. Ce guide vous présente deux options différentes pour inclure des polices Web dans votre projet.

## Utilisation d'un fichier local

Si vous souhaitez ajouter des fichiers de polices à votre projet, nous vous recommandons de les ajouter dans le [fichier `public/`](/fr/core-concepts/project-structure/#public). Dans votre CSS, vous pouvez alors enregistrer les polices avec une [déclaration `@font-face`](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face) et utiliser `font-family` pour rajouter la police à votre texte.

### Exemple

Imaginons que vous ayez un fichier de police `DistantGalaxy.woff`.

1. Rajoutez votre fichier à `public/fonts/`.

2. Rajouter `@font-face` dans votre CSS. Ceci pourais être dans un fichier global `.css` que vous importez ou un block `<style>` dans le layout ou component de votre choix.

    ```css
    /* Enregistrer notre famille de polices personnalisée et indiquer au navigateur où la trouver. */
    @font-face {
      font-family: 'DistantGalaxy';
      src: url('/fonts/DistantGalaxy.woff') format('woff');
      font-weight: normal;
      font-style: normal;
      font-display: swap;
    }
    ```

    :::note
    On n'inclus pas `public` dans l'URL source de la police, car tous les fichiers de `public` sont rajoutés au fichier racine.
    :::

3. Utilisez `font-family` de la déclaration `@font-face` pour rajouter la police au component ou layout. Dans cet exemple, la déclaration `<h1>` va avoir la police rajoutés, alors que la déclaration `<p>` ne l'auras pas.

    ```astro {10-12}
    ---
    // src/pages/example.astro
    ---

    <h1>Dans une galaxie très, très lointaine...</h1>

    <p>Les polices personnalisées rendent mes en-têtes beaucoup plus cool !</p>

    <style>
    h1 {
      font-family: 'DistantGalaxy', sans-serif;
    }
    </style>
    ```

## Utilisation de Fontsource

Le projet [Fontsource](https://fontsource.org/) simplifie l'utilisation de Google Fonts et d'autres polices open source. Il fournit les modules npm que vous pouvez installer pour les polices que vous souhaitez utiliser.

1. Trouvez la police que vous souhaitez dans le [catalogue Fontsource](https://fontsource.org/fonts). Pour cet exemple, on utilisera la police [Twinkle Star](https://fontsource.org/fonts/twinkle-star).

2. Installez le paquet pour la police que vous avez choisie.

    <PackageManagerTabs>
      <Fragment slot="npm">
      ```shell
      npm i @fontsource/twinkle-star
      ```
      </Fragment>
      <Fragment slot="pnpm">
      ```shell
      pnpm i @fontsource/twinkle-star
      ```
      </Fragment>
      <Fragment slot="yarn">
      ```shell
      yarn add @fontsource/twinkle-star
      ```
      </Fragment>
    </PackageManagerTabs>

    :::tip
    Vous trouverez le nom correct du paquetage dans la section "Quick Installation" de chaque page de police sur le site Web de Fontsource. Il commencera par `@fontsource/` suivi du nom de la police.
    :::

3. Importez le pack de polices dans le layout ou le component où vous souhaitez utiliser la police. En général, il est préférable d'effectuer cette opération dans un component de layout commun afin de s'assurer que la police est disponible sur l'ensemble du site.

    L'importation ajoutera automatiquement les déclarations `@font-face` nécessaires pour la police.

    ```astro
    ---
    // src/layouts/BaseLayout.astro
    import '@fontsource/twinkle-star';
    ---
    ```

4. Utilisez la déclaration `font-family` comme indiqué sur la page Fontsource de cette police. Cela fonctionnera partout où vous pouvez écrire du CSS dans votre projet Astro.

    ```css
    h1 {
      font-family: "Twinkle Star", cursive;
    }
    ```

## Ressources Additionelles

### Rajoutez des polices avec TailwindCSS

Si vous utilisez l'intégration [Tailwind](/fr/guides/integrations-guide/tailwind/), vous pouvez sois rajouter la déclaration `@font-face` pour une police locale ou utilisez la statégie `import` de Fontsource pour utiliser la police. Ensuite, suivez la [documentation sur l'ajout de familles de polices personnalisées Tailwind](https://tailwindcss.com/docs/font-family#using-custom-values).

### Apprenez comment fonctionnent les polices de caractères sur Internet

[Le guide des polices web MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts) introduit le sujet.

### Générer un CSS pour votre police

[le générateur de police Web Font Squirrel](https://www.fontsquirrel.com/tools/webfont-generator) peut aider à préparer vos fichiers de police pour vous.
