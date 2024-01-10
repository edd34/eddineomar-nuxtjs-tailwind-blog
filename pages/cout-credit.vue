<template>
  <div class="max-w-3xl px-4 mx-auto sm:px-6 xl:max-w-5xl xl:px-0">
    <div class="pt-6 pb-8 space-y-2 md:space-y-5">
      <h1
        class="text-3xl font-extrabold leading-9 tracking-tight text-gray-900 dark:text-gray-100 sm:text-4xl sm:leading-10 md:text-6xl md:leading-14"
      >
        Calcul du coût du crédit et montant des mensualités
      </h1>
      <p class="text-lg leading-7 text-gray-500 dark:text-gray-400">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Atque
        perspiciatis est similique blanditiis architecto possimus libero maiores
        laudantium assumenda impedit, vero, excepturi enim itaque asperiores
        quos iusto minus. Dolorum, et!
      </p>
      <p>
        Cet outil permet calculer le coût du crédit et le montant des
        mensualités !
      </p>
      <a href="">Source</a>
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
        👉 Paiement mensuel = {{ this.format_euro(this.paiement_mensuel) }}
      </div>
      <div>
        👉 Coût total prêt = {{ this.format_euro(this.cout_total_pret) }}
      </div>
      <div>
        👉 Coût total intérêts = {{ this.format_euro(this.cout_total_interet) }}
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          name: "montant_total",
          param: "Prix bien (€)",
          description: "Le prix de votre bien immobilier en €.",
          valeur: 190000,
          step: 10000,
        },
        {
          name: "apport",
          param: "Montant apport (€)",
          description: "Saisissez le montant de votre apport en €.",
          valeur: 20000,
          step: 5000,
        },
        {
          name: "taux_interet_annuel",
          param: "Taux d'intérêt",
          description:
            "Saisissez le taux d'intérêt accordé par la banque en %.",
          valeur: 4.5,
          step: 0.7,
        },
        {
          name: "duree_pret",
          param: "Durée du prêt (année)",
          description:
            "Saisissez en combien d'annéees vous souhaitez rembourser le prêt",
          valeur: 20,
          step: 5,
        },
        {
          name: "frais_notaire",
          param: "Frais notaire : 8% ancien, 3% neuf",
          valeur: 8,
          step: 1,
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
        minimumFractionDigits: 0,
        maximumFractionDigits: 2,
      }).format(num);
    },
  },
  computed: {
    taux_interet_mensuel() {
      return this.get_property_value("taux_interet_annuel") / 100 / 12;
    },
    total_paiement() {
      return this.get_property_value("duree_pret") * 12;
    },
    paiement_mensuel() {
      var result =
        (this.taux_interet_mensuel *
          (this.get_property_value("montant_total") *
            (1 + this.get_property_value("frais_notaire")/100) -
            this.get_property_value("apport"))) /
        (1 - (1 + this.taux_interet_mensuel) ** -this.total_paiement);
      return result;
    },
    cout_total_pret() {
      return this.paiement_mensuel * this.total_paiement;
    },
    cout_total_interet() {
      return (
        this.cout_total_pret -
        (this.get_property_value("montant_total") *
          (1 + this.get_property_value("frais_notaire")/100) -
          this.get_property_value("apport"))
      );
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
