# Philippine Evacuation Centers Dataset
Evacuation Centers and Shelters Dataset in the Philippines. In all honesty, I made this dataset to finish a school project and I wondered why is there no central dataset for evacuation centers in the Philippines. With this being said, I publish this dataset to the public to help others who might need it.

> [!IMPORTANT]
> The dataset might not cover all evacuation centers and shelters in the Philippines. It may also include some outdated information since it was only pulled from OSM. Please use with caution. You may contribute to this dataset by [submitting a pull request](https://github.com/cifelse/ph-evac-centers/pulls).

## Origin
The evacuation center dataset was retrieved using the [Overpass Turbo API](https://overpass-turbo.eu/) (a web-based data filtering tool for [OpenStreetMap](https://www.openstreetmap.org/)) with the following query:
```
[out:json][timeout:25];

{{geocodeArea:Philippines}}->.searchArea;
(
  node["social_facility"="shelter"](area.searchArea);
  way["social_facility"="shelter"](area.searchArea);
  relation["social_facility"="shelter"](area.searchArea);

  node["social_facility:for"="displaced"](area.searchArea);
  way["social_facility:for"="displaced"](area.searchArea);
  relation["social_facility:for"="displaced"](area.searchArea);

  node["emergency:social_facility"="shelter"](area.searchArea);
  way["emergency:social_facility"="shelter"](area.searchArea);
  relation["emergency:social_facility"="shelter"](area.searchArea);

  node["emergency:social_facility:for"="displaced"](area.searchArea);
  way["emergency:social_facility:for"="displaced"](area.searchArea);
  relation["emergency:social_facility:for"="displaced"](area.searchArea);
);

out body;
>;
out skel qt;
```

## Files Included
I exported the files in GeoJSON format as I assume that it will be beneficial to visualize this using GeoPandas. However, it is easy to load it using vanilla pandas. With this being said, the repository includes the following files:
1. `ph_evacs_raw.geojson` - The raw dataset queried from OSM.
2. `ph_evacs_cleaned.geojson` - The cleaned dataset.
3. `main.ipynb` - The Jupyter Notebook used to clean the dataset.

## Data Dictionary
The cleaned dataset includes the following columns:
1. `id` - The unique identifier of the evacuation center.
2. `name` - The name of the evacuation center.
3. `city` - The city where the evacuation center is located.
4. `municipality` - The municipality where the evacuation center is located.
5. `place` - The place where the evacuation center is located.
6. `province` - The province where the evacuation center is located.
7. `capacity` - The capacity of the evacuation center.
8. `type` - The type of evacuation center.
9. `geometry` - The geometry of the evacuation center.

## Types of Evacuation Centers
In the cleaned dataset, the evacuation centers are classified into the following types:
1. `Barangay Hall` - A barangay hall that can be used as an evacuation center.
2. `Campus` - A daycare, elementary, school, college, or university that can be used as an evacuation center.
3. `Church` - A church or place of worship that can be used as an evacuation center.
4. `Field` - An open field that can be used as an evacuation center.
5. `Hospital` - A hospital, medical center, clinic that can be used as an evacuation center.
6. `Shelter` - A dedicated shelter or evacuation center.
7. `Sports Center` - A covered court, sports complex, or sports center that can be used as an evacuation center.

## Suggestions and Contributions
As mentioned above, the dataset might not be complete and may contain outdated information. If you have any suggestions or contributions, please feel free to submit a pull request. I would be happy to review and merge them. It's alright if you're just going to add one evacuation center or shelter. Every contribution counts.
