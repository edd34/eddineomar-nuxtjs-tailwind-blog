<template>
  <div class="max-w-3xl px-4 mx-auto sm:px-6 xl:max-w-5xl xl:px-0">
    <div class="pt-6 pb-8 space-y-2 md:space-y-5">
      <h1
        class="text-3xl font-extrabold leading-9 tracking-tight text-gray-900 dark:text-gray-100 sm:text-4xl sm:leading-10 md:text-6xl md:leading-14"
      >
        Simulation ROI Panneau Solaire
      </h1>
      <p class="text-lg leading-7 text-gray-500 dark:text-gray-400">
        L'objectif de cet outil est de permettre à chacun de simuler en
        utilisant les principaux paramètres de choix de pour l'investissement
        dans un système solaire. Les paramètes sont remis par défaut à chaque
        actualisation de la page. Les paramètes par défaut sont sélectionnés
        pour Mayotte.
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
          👉 Quantité d'énergie produite :
          <b>
            {{ this.format_number(quantite_produite_par_an) }}
            kWh
          </b>
        </div>

        <div>
          👉 Facture énergie actuelle par an :
          <b>
            {{ this.format_euro(year_power_invoice) }}
          </b>
        </div>

        <div
          v-if="quantite_produite_par_an > this.get_property_value('kwh_conso')"
        >
          👉 Vous économiserez :
          <b> {{ this.format_euro(year_power_invoice) }} par an</b>. En gros
          vous ne paierez pas l'énergie électrique consommée la journée dans
          votre foyer.
        </div>
        <div v-else>
          👉 Vous économiserez :
          <b>
            {{ this.format_euro(year_power_invoice_generated_power) }} par an </b
          >par rapport à votre facture d'énergie actuelle
        </div>

        <div
          v-if="quantite_produite_par_an > this.get_property_value('kwh_conso')"
        >
          👉 Si vous revendez votre énergie, vous gagnerez
          <b> {{ this.format_euro(revenu_revente) }} par an.</b>
        </div>
        <div>
          👉 Montant à investir :
          <b> {{ this.format_euro(investissement_intial) }}</b>
        </div>
        <div>
          👉 Surface de l'installation :
          <b>
            {{
              this.format_number(
                this.get_property_value("nb_solar_panel") *
                  this.get_property_value("area_solar_panel")
              )
            }}
            m²
          </b>
        </div>
        <div
          v-if="quantite_produite_par_an > this.get_property_value('kwh_conso')"
        >
          👉 Vous êtes rentables en
          <b> {{ this.format_number(seuil_renta) }} an</b>*.
        </div>
        <div v-else>👉 Vous n'êtes pas encore rentable</div>
      </div>
      <br />
      * Attention, ce calcul est indicatif, ne tient pas compte des frais
      d'achat de composants annexes au système solaire (onduleur, cable, frais
      de ports etc..) ni des éléments fiscaux.
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          name: "kwh_conso",
          param: "kWh / an",
          description:
            "Saisissez le nombre de kWh consommés en une année dans votre foyer",
          valeur: 5000,
          step: 100,
        },
        {
          name: "nb_hour_sunlight",
          param: "Nb heure ensoleillement",
          description: "Saisissez le nombre d'heure d'ensoleillement",
          valeur: 2863,
          step: 50,
        },
        {
          name: "solar_panel_power",
          param: "Puissance panneau solaire",
          description: "Saisissez la puissance du panneau solaire (en kW)",
          valeur: 0.53,
          step: 0.1,
        },
        {
          name: "solar_panel_price",
          param: "Prix panneau solaire",
          description: "Saisissez prix du panneau solaire",
          valeur: 121.9,
          step: 20,
        },
        {
          name: "area_solar_panel",
          param: "Surface du panneau solaire",
          description: "Saisissez la surface du panneau solaire en m²",
          valeur: 2.19,
          step: 0.1,
        },
        {
          name: "coeff_loss",
          param: "Coefficient de pertes",
          description:
            "Coefficient qui correspond aux pertes dans les câbles et dû à la conversion de l'énergie",
          valeur: 0.7,
          step: 0.01,
        },
        {
          name: "kwh_price_in_euro",
          id: 8,
          param: "Prix du kWh en euro",
          description: "Saissez le prix moyen du kWh en vigueur en euro",
          valeur: 0.09,
          step: 0.01,
        },
        {
          name: "kwh_price_in_euro_sell",
          id: 8,
          param: "Prix du rachat du kWh",
          description:
            "Saissez le prix moyen du rachat de l'excédent du kWh par votre fournisseur d'énergie",
          valeur: 0.18,
          step: 0.01,
        },
        {
          name: "nb_solar_panel",
          param: "Nb panneaux solaires",
          description:
            "Saissez le nombre de panneaux solaire dans votre installation",
          valeur: 5,
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
  },
  computed: {
    revenu_revente() {
      return (
        (this.quantite_produite_par_an - this.get_property_value("kwh_conso")) *
        this.get_property_value("kwh_price_in_euro_sell")
      );
    },
    quantite_produite_par_an() {
      return (
        this.get_property_value("nb_solar_panel") *
        this.get_property_value("coeff_loss") *
        this.get_property_value("solar_panel_power") *
        this.get_property_value("nb_hour_sunlight")
      );
    },
    year_power_invoice() {
      return (
        this.get_property_value("kwh_conso") *
        this.get_property_value("kwh_price_in_euro")
      );
    },
    year_power_invoice_generated_power() {
      return (
        this.quantite_produite_par_an *
        this.get_property_value("kwh_price_in_euro")
      );
    },
    energy_saving() {
      return (
        this.get_property_value("nb_solar_panel") *
        this.get_property_value("coeff_loss") *
        this.get_property_value("solar_panel_power") *
        this.get_property_value("nb_hour_sunlight") *
        this.get_property_value("kwh_price_in_euro")
      );
    },
    investissement_intial() {
      return (
        this.get_property_value("nb_solar_panel") *
        this.get_property_value("solar_panel_price")
      );
    },
    seuil_renta() {
      return (
        this.investissement_intial /
        (this.year_power_invoice + this.revenu_revente)
      );
    },
  },

  head: {
    title: "🚀 Eddine OMAR | Calculatrice ROI photovoltaique",
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
