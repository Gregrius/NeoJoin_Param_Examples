
# Car Infotainment System Example

A set of examples demonstrating for using [NeoJoin](https://github.com/vitruv-tools/NeoJoin) in the context of Software Product Lines.

The examples are based on a hypothetical Car Infotainment System scenario with the following Feature Model:

![Feature Model](diagram/CarInfotainment_feature_diagram.png)

## Structure

- metamodels - various metamodels (in ecore format) used in the example
- instances - XMI model instances, including the feature model
- parameters - XMI files defining the Basic and Comfort configurations - used as parameters in the NeoJoin queries
- queries - sample NeoJoin queries
- dagram - an Eclipse / FeatureIDE project for visualisation of the feature diagram

## Examples

### Example - Stakeholder-specific view

The goal is to generate a view that exposes only the model elements relevant to a specific role or concern, without modifying the underlying model.

The example query combines SysML and CAD elements from the 150% model to generate a view for an architect.

Run:

```neojoin car-infotainment/queries/architecture_view.nj -m car-infotainment/metamodels -i car-infotainment/instances -t car-infotainment/queries_results/architecture_view_result.xmi```


### Example - Configuration-specific views

The goal is to generate a view which contains only the elements associated with a specific product configuration / a selection of features.

#### Example - BOM filtered by feature list

Bill of Materials for a selection of features
- Demonstrates the `param` keyword solving the SPL filtering problem
- The `activeFeatures` parameter receives a list of features for a specific product configuration

- When executed with Base Model (`features_base_model.xmi`) as a parameter -> 9 blocks (BaseSystem + RadioTuner + SmartphoneIntegration + AppleCarPlay + AndroidAuto)
- When executed with Comfort Model (`features_comfort_model.xmi`) as a parameter -> 13 blocks (adds NavigationSystem + BasicNavigation + OfflineMapStorage + DriverAssistanceDisplay)

Run

```neojoin car-infotainment/queries/bom_by_feature_list.nj -m car-infotainment/metamodels -i car-infotainment/instances -p activeFeatures=car-infotainment/parameters/features_base_model.xmi -t car-infotainment/queries_results/bom_for_featureList_base_result.xmi```

```neojoin car-infotainment/queries/bom_by_feature_list.nj -m car-infotainment/metamodels -i car-infotainment/instances -p activeFeatures=car-infotainment/parameters/features_comfort_model.xmi -t car-infotainment/queries_results/bom_for_featureList_comfort_result.xmi```


#### Example - BOM filtered by Configuration object

Bill of Materials for a product configuration

- Demonstrates the `param` keyword solving the SPL filtering problem, using a Configuration as input
- The param `activeConfig` receives the specific configuration (an instance of the configurations model) as xmi

Run

```neojoin car-infotainment/queries/bom_by_configuration.nj -m car-infotainment/metamodels -i car-infotainment/instances -p activeConfig=car-infotainment/parameters/config_base_model.xmi -t car-infotainment/queries_results/bom_using_config_base_result.xmi```

### Example - Feature module view

The goal is to retrieve all model elements belonging to a specific feature.
The feature is provided via parameter at execution time.

The concrete example takes a feature name as a parameter and creates a view containing all SysML blocks related to this feature.

- Run with `featureName=NavigationSystem` -> INavigationService, NavigationService
- Run with `featureName=BasicNavigation` -> BasicMapRenderer
- Run with `featureName=PremiumNavigation` -> PremiumMapRenderer

Run

```neojoin car-infotainment/queries/blocks_for_feature.nj -m car-infotainment/metamodels -i car-infotainment/instances -p featureName=NavigationSystem -t car-infotainment/queries_results/components_for_feature_NavigationSystem_result.xmi```

```neojoin car-infotainment/queries/blocks_for_feature.nj -m car-infotainment/metamodels -i car-infotainment/instances -p featureName=BasicNavigation -t car-infotainment/queries_results/components_for_feature_BasicNavigation_result.xmi```

```neojoin car-infotainment/queries/blocks_for_feature.nj -m car-infotainment/metamodels -i car-infotainment/instances -p featureName=PremiumNavigation -t car-infotainment/queries_results/components_for_feature_PremiumNavigation_result.xmi```

### Example - Variability infused views

The following examples demonstrate how the templates could be used to add variability information to existing views.

#### Example - using the feature name template

This example uses the [/templates/feature_name_template.nj](/templates/feature_name_template.nj) to combine information from the SysML model with the corresponding feature name.

The concrete query (after replacing the placeholders) is `blocks_with_feature_names.nj`.

Run

```neojoin car-infotainment/queries/blocks_with_feature_names.nj -m car-infotainment/metamodels -i car-infotainment/instances -t car-infotainment/queries_results/blocks_with_feature_names_result.xmi```

#### Example - using the feature type template