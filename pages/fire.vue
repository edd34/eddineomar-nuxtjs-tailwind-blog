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
        Simulation FIRE
      </h1>
      <p class="text-lg leading-7 text-gray-500 dark:text-gray-400">
        Le mouvement FIRE, de l'acronyme anglais financial independence, retire
        early, ou en français « indépendance financière, retraite précoce » est
        un mouvement dont l'objectif est l'indépendance financière et la
        retraite anticipée. Le modèle est particulièrement populaire parmi les
        membres de la génération Y et gagne du terrain à travers les communautés
        en ligne via l'information partagée dans les blogs, les podcasts et les
        forums de discussion en ligne.
      </p>
      <a href="https://www.wikiwand.com/fr/Mouvement_FIRE"
        >Cf Mouvement FIRE sur Wikipedia.</a
      >
      <p>
        Cet outil permet de simuler la date de fire à l'aide de quelques
        paramètres.
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
        👉 Il vous faut accumuler
        <b>
          {{
            this.format_euro(
              (this.get_property_value("charges") * 12 * 100) /
                this.get_property_value("roi_per_year")
            )
          }}
        </b>
        pour obtenir une rente de
        <b>
          {{ this.format_euro(this.get_property_value("charges")) }} par mois
        </b>
        avec un placement à
        <b
          >{{
            this.format_percentage(
              this.get_property_value("roi_per_year") / 100
            )
          }}

          par an</b
        >.
      </div>
      <div>
        👉 Vous pourrez vivre de vos rentes dans
        <b> {{ this.format_number(this.fire.year) }} ans </b>.
      </div>
      <div>
        👉 Vous aurez accumulé un capital
        <b>{{ this.format_euro(this.fire.capital) }} au moment du FIRE.</b>.
      </div>
      <div>
        👉 Vous atteindrez
        <b>
          {{
            new Intl.NumberFormat("fr-FR", {
              style: "currency",
              notation: "compact",
              compactDisplay: "short",
              currency: "EUR",
            }).format(this.get_property_value("capital_dream"))
          }}
        </b>
        de capital dans
        <b>{{ this.format_number(this.fire_goal.year) }} ans</b>.
      </div>
      <br />
      * Attention, ce calcul est indicatif. Investir comporte des risques dont
      la perte total du capital investi.
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          name: "salaire_mensuel",
          param: "Salaire / mois",
          description: "Indiquez vitre salaire mensuel net.",
          valeur: 2500,
          step: 100,
        },
        {
          name: "charges",
          param: "Charges / mois",
          description: "Saisissez le montant de vos charges mensuelles.",
          valeur: 1300,
          step: 50,
        },
        {
          name: "roi_per_year",
          param: "ROI moyen du placement",
          description:
            "Saissez le rendement moyen espéré de votre placement. Ex : 4%",
          valeur: 4,
          step: 1,
        },
        {
          name: "inital_amount",
          param: "Somme de départ",
          description:
            "Indiquez le montant de l'épargne dont vous disposez déjà.",
          valeur: 0,
          step: 1000,
        },
        {
          name: "capital_dream",
          param: "Capital de rêve",
          description:
            "Indiquez le montant du capital dont vous souhaitez obtenir.",
          valeur: 100000,
          step: 10000,
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
  },
  computed: {
    saving_per_month() {
      return (
        this.get_property_value("salaire_mensuel") -
        this.get_property_value("charges")
      );
    },
    saving_per_year() {
      return this.saving_per_month * 12;
    },
    fire() {
      var n = 1;
      var u0 = this.get_property_value("inital_amount");
      var capital = u0;
      while (
        (this.get_property_value("roi_per_year") / 100) * capital <
        this.get_property_value("charges") * 12
      ) {
        n += 1;
        capital =
          capital * (1 + this.get_property_value("roi_per_year") / 100) +
          this.saving_per_year;
      }

      return {
        year: n,
        capital: capital,
        roi_capital: (capital * this.get_property_value("roi_per_year")) / 100,
      };
    },
    fire_goal() {
      var n = 1;
      var u0 = this.get_property_value("inital_amount");
      var capital = u0;
      while (capital < this.get_property_value("capital_dream")) {
        n += 1;
        capital =
          capital * (1 + this.get_property_value("roi_per_year") / 100) +
          this.saving_per_year;
      }

      return {
        year: n,
        capital: capital,
        roi_capital: (capital * this.get_property_value("roi_per_year")) / 100,
      };
    },
  },

  head: {
    title: "🚀 Eddine OMAR | 🚧 Calculatrice FIRE 🚧",
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
