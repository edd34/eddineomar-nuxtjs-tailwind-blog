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
        Simulation rentabilité immobilier locatif
      </h1>
      <p class="text-lg leading-7 text-gray-500 dark:text-gray-400">
        La rentabilité mesure la performance d'un investissement locatif. 

        Un placement, c'est fait pour être rentable.
        Par exemple, vous placez 100 €. Un an plus tard, vous avez 104 €.
        L'opération vous rapporte donc 4 % par an.
        En matière d'investissement immobilier, il s'agit de connaître votre rendement locatif.
        Grosso modo, c'est le ratio entre ce que vous rapporte le logement que vous louez (loyers) et ce qu'il vous coûte (prix d'achat, crédit, entretien, taxes, etc.).
        Pour ce qui vous concerne, en tant qu'investisseur, la question prend une importance cruciale puisque votre opération immobilière ne doit pas vous faire perdre d'argent. 
      </p>
      <p>
        Cet outil permet de simuler la rentabilité d'un bien immobilier en fonction de quelques paramètres.
      </p>
      <a href="https://www.pap.fr/bailleur/choisir-investissement/immobilier-locatif-jusqu-a-7-de-rentabilite/a1263">Source</a>
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
        👉 Loyer annuel = {{this.format_euro(this.get_property_value("loyer"))}} * 12 = {{this.format_euro(this.loyer_an)}}
      </div>
      <div>
        👉 Formule rentabilité brute = {{this.format_euro(this.loyer_an)}} / {{this.format_euro(this.get_property_value("prix"))}}
      </div>
      <div>
        👉 <b> Rentabilité brute = {{this.format_percentage(this.loyer_an/this.get_property_value("prix"))}}</b>
      </div>
      <div>
        👉 Formule rentabilité nette = ({{this.format_euro(this.loyer_an)}} - {{this.format_euro(this.get_property_value("charges_copro"))}} - {{this.format_euro(this.get_property_value("taxe_fonciere"))}}) / ({{this.format_euro(this.get_property_value("prix"))}}*(1 + {{this.get_property_value("p_frais_agence")}}% + {{this.get_property_value("p_frais_notaire")}}%) + {{this.format_euro(this.get_property_value("travaux"))}})
      </div>
      <div>
        <b>
          👉 Rentabilité nette = {{this.format_percentage(this.rentabilite_nette)}}
        </b>
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
          name: "prix",
          param: "Prix",
          description: "Le prix de votre bien immobilier en €.",
          valeur: 170000,
          step: 10000,
        },
        {
          name: "loyer",
          param: "Loyer du bien immobilier.",
          description: "Saisissez le montant du loyer du bien immobilier.",
          valeur: 750,
          step: 50,
        },
        {
          name: "charges_copro",
          param: "Montant des charges de copro",
          description:
            "Saisissez la valeur des charges annuelles de copropriété",
          valeur: 900,
          step: 50,
        },
        {
          name: "taxe_fonciere",
          param: "Taxe foncière",
          description:
            "Saisissez le montant annuel de la taxe foncière en €.",
          valeur: 700,
          step: 50,
        },
        {
          name: "travaux",
          param: "Montant des travaux",
          description: "Indiquez le montant des travaux en €.",
          valeur: 7000,
          step: 1000,
        },
        {
          name: "p_frais_agence",
          param: "Frais d'agence",
          description: "Indiquez le pourcentage des frais d'agence en %.",
          valeur: 5,
          step: 0.5,
        },
        {
          name: "p_frais_notaire",
          param: "Frais de notaire",
          description: "Indiquez le pourcentage des frais de notaires.",
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
        maximumFractionDigits: 2
      }).format(num);
    },
  },
  computed: {
    loyer_an() {
      return (
        this.get_property_value("loyer")*12
      );
    },
    rentabilite_nette() {
      return (
        (this.get_property_value("loyer")*12 - this.get_property_value("taxe_fonciere") - this.get_property_value("charges_copro")) 
        / 
        (this.get_property_value("prix") * (1 + this.get_property_value("p_frais_notaire")/100 + this.get_property_value("p_frais_agence")/100) + this.get_property_value("travaux"))
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
