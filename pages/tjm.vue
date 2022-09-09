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
        Simulation CA freelance
      </h1>
      <p class="text-lg leading-7 text-gray-500 dark:text-gray-400">
        Le CA d'un freelance correspond à la rémunération brute qu'il va
        facturer à l'ensemble de ses clients. Il faut savoir que le CA est
        soumis à diverses taxes qui seront versées à un organisme tel que
        l'URSSAF.
      </p>
      <p>
        Cet outil permet de simuler le CA annuel en fonction du TJM et du nombre
        de jours non travaillé.
      </p>
    </div>
    <main class="relative mb-auto">
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
              <template v-slot="props">
                <b-numberinput
                  v-model="props.row.valeur"
                  :step="props.row.step"
                  controls-position="compact"
                ></b-numberinput>
              </template>
            </b-table-column>
          </b-table>
        </section>
      </div>
      Résultat :
      <div>
        👉 Vous allez travailler <b> {{ nb_jour_travaille }}</b> jours par an.
      </div>
      <div>
        👉 Vous réaliserez un CA brut de
        <b> {{ this.format_euro(this.CA_an_brut) }} / an</b> soit
        <b> {{ this.format_euro(this.CA_mois_brut) }} brut / mois</b>
      </div>
      <div>
        👉 Vous réaliserez un CA net de
        <b> {{ this.format_euro(this.CA_an_net("rate_micro")) }} / an</b> en
        micro entreprise. Soit
        <b>
          {{ this.format_euro(this.CA_mois_net("rate_micro")) }} net / mois</b
        >
      </div>
      <!-- <div>
        👉 Vous réaliserez un CA net de
        <b> {{ this.format_euro(this.CA_an_net("rate_eurl_sarl")) }} / an</b> en
        société.
      </div> -->
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          name: "TJM",
          param: "TJM Consulting",
          description: "Indiquez votre TJM.",
          valeur: 550,
          step: 50,
        },
        {
          name: "nb_jour_ouvres",
          param: "Nombre de jours ouvrés",
          description: "Saisissez le montant de jours ouvrés par an.",
          valeur: 251,
          step: 1,
        },
        {
          name: "conges",
          param: "Nb de jour non travailles",
          description:
            "Comptez le nombre de jour de congés ainsi que les intercontrats",
          valeur: 25,
          step: 1,
        },
        {
          name: "rate_micro",
          param: "Taux de prélèvement",
          description:
            "Indiquez le montant du capital dont vous souhaitez obtenir.",
          valeur: 0.242,
          step: 0.01,
        },
        {
          name: "rate_eurl_sarl",
          param: "Taux de prélèvement",
          description:
            "Indiquez le montant du capital dont vous souhaitez obtenir.",
          valeur: 0.44,
          step: 0.01,
        },
      ],
    };
  },
  methods: {
    get_property_value(property_tag) {
      return this.data.find((x) => x.name == property_tag).valeur;
    },
    format_euro(num) {
      return new Intl.NumberFormat(`fr-FR`, {
        currency: `EUR`,
        style: "currency",
      }).format(num);
    },
    format_number(num) {
      return new Intl.NumberFormat(`fr-FR`, {
        maximumFractionDigits: 2,
      }).format(num);
    },
    format_percentage(num) {
      return new Intl.NumberFormat("fr-FR", {
        style: "percent",
      }).format(num);
    },
    CA_an_net(regime) {
      return this.CA_an_brut * (1 - this.get_property_value(regime));
    },
    CA_mois_net(regime) {
      return this.CA_mois_brut * (1 - this.get_property_value(regime));
    },
  },
  computed: {
    nb_jour_travaille() {
      return (
        this.get_property_value("nb_jour_ouvres") -
        this.get_property_value("conges")
      );
    },
    CA_an_brut() {
      return this.get_property_value("TJM") * this.nb_jour_travaille;
    },
    CA_mois_brut() {
      return (this.get_property_value("TJM") * this.nb_jour_travaille) / 12;
    },
  },

  head: {
    title: "🚀 Eddine OMAR | 🚧 Calculatrice TJM 🚧",
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
