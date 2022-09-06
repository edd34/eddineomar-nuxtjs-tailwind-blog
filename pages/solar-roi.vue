<template>
  <div class="max-w-3xl px-4 mx-auto sm:px-6 xl:max-w-5xl xl:px-0">
    <div class="pt-6 pb-8 space-y-2 md:space-y-5">
      <h1
        class="
          text-3xl
          font-extrabold
          leading-9
          tracking-tight
          text-gray-900
          dark:text-gray-100
          sm:text-4xl sm:leading-10
          md:text-6xl md:leading-14
        "
      >
        Calcul ROI Panneau Solaire à Mayotte
      </h1>
      <p class="text-lg leading-7 text-gray-500 dark:text-gray-400">
        Je suis constamment en train de m'autoformer, de hacker un programme ou
        en train de développer un projet. Je vous partage une partie des projets
        intéressants que j'ai réalisés. Côté technos : je travaille souvent avec
        Python, Django, Flask, Git, Github, Vue/Nuxt et TailwindCSS. Il y a
        également des projets cryptos avec web3py, solidity et plein d'autres à
        venir !
      </p>
    </div>
    <main class="relative mb-auto">
      <div class="">
        <div class="container py-12">
          <section>
            <b-table :data="data">
              <b-table-column field="user.param" label="Paramètre">
                <template v-slot:header="{ column }">
                  <b-tooltip :label="column.label" append-to-body dashed>{{
                    column.label
                  }}</b-tooltip>
                </template>
                <template v-slot="props">{{ props.row.param }}</template>
              </b-table-column>
              <b-table-column field="user.description" label="Description">
                <template v-slot:header="{ column }">
                  <b-tooltip :label="column.label" append-to-body dashed>{{
                    column.label
                  }}</b-tooltip>
                </template>
                <template v-slot="props">{{ props.row.description }}</template>
              </b-table-column>
              <b-table-column field="user.valeur" label="Valeur">
                <template v-slot:header="{ column }">
                  <b-tooltip :label="column.label" append-to-body dashed>{{
                    column.label
                  }}</b-tooltip>
                </template>
                <template v-slot="props">
                  <b-numberinput
                    v-model="props.row.valeur"
                    controls-position="compact"
                    :editable="false"
                  ></b-numberinput>
                </template>
              </b-table-column>
            </b-table>
          </section>
        </div>
        <div>Facture énergie an : {{ year_power_invoice }} €</div>
        <div>Vous avez économisé : {{ energy_saving }} €</div>
        <div>
          Montant à investir :
          {{ investissement_intial }} €
        </div>
        <div>Vous êtes rentables en {{ seuil_renta }} an</div>
      </div>
    </main>
    <p class="text-m leading-7 text-gray-500 dark:text-gray-400 italic">
      PSSST!? Au fait, ça vous dirait d'aller mettre des 🌟 dans mes projets
      perso sur Github ?
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          name: "kwh_conso",
          id: 1,
          param: "kWh / an",
          description:
            "Saisissez le nombre de kWh consommés en une année dans votre foyer",
          valeur: 5000,
        },
        {
          name: "nb_hour_sunlight",
          id: 2,
          param: "Nb heure ensoleillement",
          description: "Saisissez le nombre d'heure d'ensoleillement",
          valeur: 2863,
        },
        {
          name: "solar_panel_power",
          id: 3,
          param: "Puissance panneau solaire",
          description: "Saisissez la puissance du panneau solaire (en W)",
          valeur: 530,
        },
        {
          name: "nb_hour_sunlight",
          id: 4,
          param: "Nb heure ensoleillement",
          description: "Saisissez le nombre d'heure d'ensoleillement",
          valeur: 2863,
        },
        {
          name: "solar_panel_price",
          id: 5,
          param: "Prix panneau solaire",
          description: "Saisissez prix du panneau solaire",
          valeur: 121.9,
        },
        {
          name: "area_solar_panel",
          id: 6,
          param: "Surface du panneau solaire",
          description: "Saisissez la surface du panneau solaire en m²",
          valeur: 2.19,
        },
        {
          name: "coeff_loss",
          id: 7,
          param: "Coefficient de pertes",
          description:
            "Coefficient qui correspond aux pertes dans les câbles et dû à la conversion de l'énergie",
          valeur: 0.7,
        },
        {
          name: "kwh_price_in_euro",
          id: 8,
          param: "Prix du kWh en euro",
          description: "Saissez le prix moyen du kWh en vigueur en euro",
          valeur: 0.14,
        },
        {
          name: "nb_solar_panel",
          id: 9,
          param: "Nb panneaux solaires",
          description:
            "Saissez le nombre de panneaux solaire dans votre installation",
          valeur: 4,
        },
      ],
    };
  },
  computed: {
    year_power_invoice() {
      return (
        this.data.find((x) => x.name == "kwh_conso").valeur *
        this.data.find((x) => x.name == "kwh_price_in_euro").valeur
      ).toFixed(2);
    },
    energy_saving() {
      return (
        ((this.data.find((x) => x.name == "nb_solar_panel").valeur *
          this.data.find((x) => x.name == "solar_panel_power").valeur) /
          1000) *
        this.data.find((x) => x.name == "nb_hour_sunlight").valeur *
        this.data.find((x) => x.name == "kwh_price_in_euro").valeur
      ).toFixed(2);
    },
    seuil_renta() {
      return (
        (this.data.find((x) => x.name == "nb_solar_panel").valeur *
          this.data.find((x) => x.name == "solar_panel_price").valeur) /
        (this.energy_saving - this.year_power_invoice)
      ).toFixed(2);
    },
    investissement_intial() {
      return (
        this.data.find((x) => x.name == "nb_solar_panel").valeur *
        this.data.find((x) => x.name == "solar_panel_price").valeur
      ).toFixed(2);
    },
  },

  head: {
    title: "🚀 Eddine OMAR | 🚧 Calculatrice 🚧",
    meta: [
      { charset: "utf-8" },
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        hid: "description",
        name: "description",
        content: "ROI Solaire Mayotte",
      },
    ],
    link: [{ rel: "icon", type: "image/x-icon", href: "/favicon.ico" }],
  },
};
</script>
