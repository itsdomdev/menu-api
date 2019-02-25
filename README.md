{
  "openapi" : "3.0.1",
  "info" : {
    "title" : "menuapi",
    "description" : "Restaurant Menus is an API providing access to a Database of over 350,000 Restaurant Menus in the US",
    "version" : "0.11"
  },
  "servers" : [ {
    "url" : "http://api.menuapi.xyz"
  } ],
  "paths" : {
    "/v1/restaurants/search/query" : {
      "get" : {
        "tags" : [ "restaurants" ],
        "summary" : "Search Restaurants By Query",
        "description" : "Returns list of by field querys with option to include full menu (limit=10) or not include full menu (limit=25)",
        "parameters" : [ {
          "name" : "q",
          "in" : "query",
          "description" : "Query String using format field:value",
          "required" : true,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "string"
          },
          "x-example" : "restaurant_name%3Awendy%2As%2Caddress.postal_code%3A11211"
        }, {
          "name" : "page",
          "in" : "query",
          "description" : "Page Number",
          "required" : false,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number",
            "default" : 1
          },
          "x-example" : 1
        }, {
          "name" : "fullmenu",
          "in" : "query",
          "description" : "Include full menus (or not)",
          "required" : false,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "boolean",
            "default" : false
          },
          "x-example" : "false"
        } ],
        "responses" : {
          "200" : {
            "description" : "OK",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/SearchResults"
                }
              }
            }
          }
        },
        "security" : [ {
          "bearerAuth" : [ ]
        }, {
          "ApiKeyAuth" : [ ]
        } ],
        "servers" : [ {
          "url" : "http://api.menuapi.xyz"
        } ]
      },
      "servers" : [ {
        "url" : "http://api.menuapi.xyz"
      } ]
    },
    "/v1/restaurants/search/location" : {
      "get" : {
        "tags" : [ "restaurants" ],
        "summary" : "Search Restaurants By Geo",
        "description" : "Search Function requiring location and search radius. Returns list of restaurants sorted by closest with option to include full menu (limit=10) or not (limit=25)",
        "parameters" : [ {
          "name" : "q",
          "in" : "query",
          "description" : "Query String using format field:value",
          "required" : false,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "string"
          },
          "example" : "pizza"
        }, {
          "name" : "distance",
          "in" : "query",
          "description" : "Search Area radius (in miles)",
          "required" : true,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number"
          },
          "example" : 5
        }, {
          "name" : "lon",
          "in" : "query",
          "description" : "Latitude of search area",
          "required" : true,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number"
          },
          "example" : -73.992378
        }, {
          "name" : "lat",
          "in" : "query",
          "description" : "Latitude of search area",
          "required" : true,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number"
          },
          "example" : 40.68919
        }, {
          "name" : "page",
          "in" : "query",
          "description" : "Page Number",
          "required" : false,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number",
            "default" : 1
          },
          "example" : 1
        }, {
          "name" : "fullmenu",
          "in" : "query",
          "description" : "Include full menus (or not)",
          "required" : false,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "boolean",
            "default" : false
          },
          "example" : "false"
        } ],
        "responses" : {
          "200" : {
            "description" : "OK",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/SearchResults"
                }
              }
            }
          }
        },
        "security" : [ {
          "bearerAuth" : [ ]
        }, {
          "ApiKeyAuth" : [ ]
        } ],
        "servers" : [ {
          "url" : "http://api.menuapi.xyz"
        } ]
      },
      "servers" : [ {
        "url" : "http://api.menuapi.xyz"
      } ]
    },
    "/v1/restaurants/{restaurant_id}" : {
      "get" : {
        "tags" : [ "restaurants" ],
        "summary" : "Get Restaurants By ID",
        "description" : "Get Single Restaurant",
        "parameters" : [ {
          "name" : "restaurant_id",
          "in" : "path",
          "description" : "Numeric ID of the restaurant to get.",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "integer",
            "format" : "int32"
          },
          "example" : 317120
        } ],
        "responses" : {
          "200" : {
            "description" : "OK",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/ResponseRest"
                }
              }
            }
          }
        },
        "security" : [ {
          "bearerAuth" : [ ]
        }, {
          "ApiKeyAuth" : [ ]
        } ],
        "servers" : [ {
          "url" : "http://api.menuapi.xyz"
        } ]
      },
      "servers" : [ {
        "url" : "http://api.menuapi.xyz"
      } ]
    },
    "/v1/menuitems/search/query" : {
      "get" : {
        "tags" : [ "menu items" ],
        "summary" : "Search menu items By Query",
        "description" : "Search Function requiring location, search radius and Keyword. Returns list of menu items that match keyword provided, sorted by closest",
        "parameters" : [ {
          "name" : "q",
          "in" : "query",
          "description" : "Query String using format field:value",
          "required" : true,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "string"
          },
          "example" : "cuisines%3Aitalian%2Caddress.postal_code%3A11211"
        }, {
          "name" : "page",
          "in" : "query",
          "description" : "Page Number",
          "required" : false,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number",
            "default" : 1
          },
          "example" : 1
        } ],
        "responses" : {
          "200" : {
            "description" : "OK",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/SearchResultsItems"
                }
              }
            }
          }
        },
        "security" : [ {
          "bearerAuth" : [ ]
        }, {
          "ApiKeyAuth" : [ ]
        } ],
        "servers" : [ {
          "url" : "http://api.menuapi.xyz"
        } ]
      },
      "servers" : [ {
        "url" : "http://api.menuapi.xyz"
      } ]
    },
    "/v1/menuitems/{item_id}" : {
      "get" : {
        "tags" : [ "menu items" ],
        "summary" : "Get Menu Item By ID",
        "description" : "Return Single Menu Item Details",
        "parameters" : [ {
          "name" : "item_id",
          "in" : "path",
          "description" : "Numeric ID of the Item to Get.",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "integer",
            "format" : "int32"
          },
          "example" : 1591156531
        } ],
        "responses" : {
          "200" : {
            "description" : "OK",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/ResponseItem"
                }
              }
            }
          }
        },
        "security" : [ {
          "bearerAuth" : [ ]
        }, {
          "ApiKeyAuth" : [ ]
        } ],
        "servers" : [ {
          "url" : "http://api.menuapi.xyz"
        } ]
      },
      "servers" : [ {
        "url" : "http://api.menuapi.xyz"
      } ]
    },
    "/v1/menuitems/search/location" : {
      "get" : {
        "tags" : [ "menu items" ],
        "summary" : "Search menu items By Geo",
        "description" : "Search Function requiring location and search radius. Returns list of menu items sorted by closest",
        "parameters" : [ {
          "name" : "q",
          "in" : "query",
          "description" : "Query String",
          "required" : false,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "string"
          },
          "example" : "pizza"
        }, {
          "name" : "distance",
          "in" : "query",
          "description" : "Search Area radius (in miles)",
          "required" : true,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number"
          },
          "example" : 5
        }, {
          "name" : "lon",
          "in" : "query",
          "description" : "Latitude of search area",
          "required" : true,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number"
          },
          "example" : -73.992378
        }, {
          "name" : "lat",
          "in" : "query",
          "description" : "Latitude of search area",
          "required" : true,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number"
          },
          "example" : 40.68919
        }, {
          "name" : "page",
          "in" : "query",
          "description" : "Page Number",
          "required" : false,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "number",
            "default" : 1
          },
          "example" : 1
        } ],
        "responses" : {
          "200" : {
            "description" : "OK",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/SearchResultsItems"
                }
              }
            }
          }
        },
        "security" : [ {
          "bearerAuth" : [ ]
        }, {
          "ApiKeyAuth" : [ ]
        } ],
        "servers" : [ {
          "url" : "http://api.menuapi.xyz"
        } ]
      },
      "servers" : [ {
        "url" : "http://api.menuapi.xyz"
      } ]
    },
    "/v1/menuitems/restaurant/{restaurant_id}" : {
      "get" : {
        "tags" : [ "menu items" ],
        "summary" : "Get menu items For Restaurant",
        "description" : "Get Menu Items For Specific Restaurant ID",
        "parameters" : [ {
          "name" : "restaurant_id",
          "in" : "path",
          "description" : "Numeric ID of the restaurant to get dishes for.",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "integer",
            "format" : "int32"
          },
          "example" : 317120
        } ],
        "responses" : {
          "200" : {
            "description" : "OK",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/SearchResultsItemsRest"
                }
              }
            }
          }
        },
        "security" : [ {
          "bearerAuth" : [ ]
        }, {
          "ApiKeyAuth" : [ ]
        } ],
        "servers" : [ {
          "url" : "http://api.menuapi.xyz"
        } ]
      },
      "servers" : [ {
        "url" : "http://api.menuapi.xyz"
      } ]
    }
  },
  "components" : {
    "schemas" : {
      "SearchResults" : {
        "required" : [ "data", "morePages", "numResults", "page", "totalPages", "totalResults" ],
        "properties" : {
          "data" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/SearchResults_data"
            }
          },
          "morePages" : {
            "type" : "boolean"
          },
          "numResults" : {
            "type" : "number",
            "example" : 25
          },
          "page" : {
            "type" : "number",
            "example" : 1
          },
          "totalPages" : {
            "type" : "number",
            "example" : 1190
          },
          "totalResults" : {
            "type" : "number",
            "example" : 29727
          }
        }
      },
      "SearchResultsItemsRest" : {
        "required" : [ "data", "morePages", "numResults", "page", "totalPages", "totalResults" ],
        "properties" : {
          "data" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/SearchResultsItemsRest_data"
            }
          },
          "morePages" : {
            "type" : "boolean"
          },
          "numResults" : {
            "type" : "number",
            "example" : 50
          },
          "page" : {
            "type" : "number",
            "example" : 1
          },
          "totalPages" : {
            "type" : "number",
            "example" : 2
          },
          "totalResults" : {
            "type" : "number",
            "example" : 96
          }
        }
      },
      "SearchResultsItems" : {
        "required" : [ "data", "morePages", "numResults", "page", "totalPages", "totalResults" ],
        "properties" : {
          "data" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/SearchResultsItems_data"
            }
          },
          "morePages" : {
            "type" : "boolean"
          },
          "numResults" : {
            "type" : "number",
            "example" : 50
          },
          "page" : {
            "type" : "number",
            "example" : 1
          },
          "totalPages" : {
            "type" : "number",
            "example" : 99867
          },
          "totalResults" : {
            "type" : "number",
            "example" : 4993309
          }
        }
      },
      "ResponseItem" : {
        "required" : [ "address", "cuisines", "geo", "item_id", "menu_item_description", "menu_item_name", "menu_item_pricing", "price_range", "restaurant_hours", "restaurant_id", "restaurant_name", "restaurant_phone", "subsection", "subsection_description" ],
        "properties" : {
          "address" : {
            "$ref" : "#/components/schemas/ResponseItem_address"
          },
          "cuisines" : {
            "type" : "array",
            "example" : [ "American (New)", "Gastropub" ],
            "items" : {
              "type" : "string"
            }
          },
          "geo" : {
            "$ref" : "#/components/schemas/ResponseItem_geo"
          },
          "item_id" : {
            "type" : "number",
            "example" : 1004304688
          },
          "menu_item_description" : {
            "type" : "string",
            "example" : "rittenhouse rye, chartreuse verde, punt e mes, orange & angostura bitters"
          },
          "menu_item_name" : {
            "type" : "string",
            "example" : "Greenback"
          },
          "menu_item_pricing" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/ResponseItem_menu_item_pricing"
            }
          },
          "price_range" : {
            "type" : "string",
            "example" : "$"
          },
          "restaurant_hours" : {
            "type" : "string",
            "example" : "Mon-Fri: 11:30am-2am  Sat: 5pm-2am"
          },
          "restaurant_id" : {
            "type" : "number",
            "example" : 341552
          },
          "restaurant_name" : {
            "type" : "string",
            "example" : "Per Diem"
          },
          "restaurant_phone" : {
            "type" : "string",
            "example" : "(415) 989-0300"
          },
          "subsection" : {
            "type" : "string",
            "example" : "New Money Cocktails"
          },
          "subsection_description" : {
            "type" : "string"
          }
        }
      },
      "ResponseRest" : {
        "required" : [ "restaurant" ],
        "properties" : {
          "restaurant" : {
            "$ref" : "#/components/schemas/ResponseRest_restaurant"
          }
        }
      },
      "SearchResults_address" : {
        "type" : "object",
        "properties" : {
          "city" : {
            "type" : "string",
            "example" : "Brooklyn"
          },
          "formatted" : {
            "type" : "string",
            "example" : "391 Henry St Brooklyn, NY 11201"
          },
          "postal_code" : {
            "type" : "string",
            "example" : "11201"
          },
          "state" : {
            "type" : "string",
            "example" : "NY"
          },
          "street" : {
            "type" : "string",
            "example" : "391 Henry St"
          }
        }
      },
      "SearchResults_geo" : {
        "type" : "object",
        "properties" : {
          "lat" : {
            "type" : "number",
            "example" : 40.688072
          },
          "lon" : {
            "type" : "number",
            "example" : -73.997385
          }
        }
      },
      "SearchResults_data" : {
        "type" : "object",
        "properties" : {
          "address" : {
            "$ref" : "#/components/schemas/SearchResults_address"
          },
          "cuisines" : {
            "type" : "array",
            "example" : [ "Alcohol", "Italian", "Tapas" ],
            "items" : {
              "type" : "string"
            }
          },
          "geo" : {
            "$ref" : "#/components/schemas/SearchResults_geo"
          },
          "hours" : {
            "type" : "string",
            "example" : "Mon-Thu: 11:30am-12am  Fri: 11:30am-2am  Sat: 10:30am-2am  Sun: 10:30am-12am"
          },
          "menus" : {
            "type" : "array",
            "example" : [ ],
            "items" : {
              "type" : "object"
            }
          },
          "price_range" : {
            "type" : "string"
          },
          "price_range_100" : {
            "type" : "number",
            "example" : 0
          },
          "restaurant_id" : {
            "type" : "number",
            "example" : 274038
          },
          "restaurant_name" : {
            "type" : "string",
            "example" : "Bocca Lupo"
          },
          "restaurant_phone" : {
            "type" : "string",
            "example" : "(718) 243-2522"
          }
        }
      },
      "SearchResultsItemsRest_address" : {
        "type" : "object",
        "properties" : {
          "city" : {
            "type" : "string",
            "example" : "BALLWIN"
          },
          "formatted" : {
            "type" : "string",
            "example" : "15483 Clayton Rd BALLWIN, MO 63011"
          },
          "postal_code" : {
            "type" : "string",
            "example" : "63011"
          },
          "state" : {
            "type" : "string",
            "example" : "MO"
          },
          "street" : {
            "type" : "string",
            "example" : "15483 Clayton Rd"
          }
        }
      },
      "SearchResultsItemsRest_geo" : {
        "type" : "object",
        "properties" : {
          "lat" : {
            "type" : "number",
            "example" : 38.608271
          },
          "lon" : {
            "type" : "number",
            "example" : -90.568715
          }
        }
      },
      "SearchResultsItemsRest_menu_item_pricing" : {
        "type" : "object",
        "properties" : {
          "currency" : {
            "type" : "string",
            "example" : "USD"
          },
          "price" : {
            "type" : "number",
            "example" : 3.95
          },
          "priceString" : {
            "type" : "string",
            "example" : "$3.95"
          }
        }
      },
      "SearchResultsItemsRest_data" : {
        "type" : "object",
        "properties" : {
          "address" : {
            "$ref" : "#/components/schemas/SearchResultsItemsRest_address"
          },
          "cuisines" : {
            "type" : "array",
            "example" : [ "American", "Pizza" ],
            "items" : {
              "type" : "string"
            }
          },
          "geo" : {
            "$ref" : "#/components/schemas/SearchResultsItemsRest_geo"
          },
          "item_id" : {
            "type" : "number",
            "example" : 79435340
          },
          "menu_item_description" : {
            "type" : "string",
            "example" : "whole button mushrooms double dipped in premium draft beer batter and served with horseradish sauce."
          },
          "menu_item_name" : {
            "type" : "string",
            "example" : "Beer Battered Mushrooms"
          },
          "menu_item_pricing" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/SearchResultsItemsRest_menu_item_pricing"
            }
          },
          "price_range" : {
            "type" : "string"
          },
          "restaurant_hours" : {
            "type" : "string"
          },
          "restaurant_id" : {
            "type" : "number",
            "example" : 57751
          },
          "restaurant_name" : {
            "type" : "string",
            "example" : "Fortel's Pizza Den"
          },
          "restaurant_phone" : {
            "type" : "string",
            "example" : "(636) 386-7199"
          },
          "subsection" : {
            "type" : "string",
            "example" : "Appetizers"
          },
          "subsection_description" : {
            "type" : "string"
          }
        }
      },
      "SearchResultsItems_address" : {
        "type" : "object",
        "properties" : {
          "city" : {
            "type" : "string",
            "example" : "Elmont"
          },
          "formatted" : {
            "type" : "string",
            "example" : "799 Elmont Rd Elmont, NY 11003"
          },
          "postal_code" : {
            "type" : "string",
            "example" : "11003"
          },
          "state" : {
            "type" : "string",
            "example" : "NY"
          },
          "street" : {
            "type" : "string",
            "example" : "799 Elmont Rd"
          }
        }
      },
      "SearchResultsItems_geo" : {
        "type" : "object",
        "properties" : {
          "lat" : {
            "type" : "number",
            "example" : 40.690643
          },
          "lon" : {
            "type" : "number",
            "example" : -73.72089
          }
        }
      },
      "SearchResultsItems_menu_item_pricing" : {
        "type" : "object",
        "properties" : {
          "currency" : {
            "type" : "string",
            "example" : "USD"
          },
          "price" : {
            "type" : "number",
            "example" : 1
          },
          "priceString" : {
            "type" : "string",
            "example" : "$1.00"
          }
        }
      },
      "SearchResultsItems_data" : {
        "type" : "object",
        "properties" : {
          "address" : {
            "$ref" : "#/components/schemas/SearchResultsItems_address"
          },
          "cuisines" : {
            "type" : "array",
            "example" : [ ],
            "items" : {
              "type" : "object"
            }
          },
          "geo" : {
            "$ref" : "#/components/schemas/SearchResultsItems_geo"
          },
          "item_id" : {
            "type" : "number",
            "example" : 539345634
          },
          "menu_item_description" : {
            "type" : "string"
          },
          "menu_item_name" : {
            "type" : "string",
            "example" : "Kid's Juice"
          },
          "menu_item_pricing" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/SearchResultsItems_menu_item_pricing"
            }
          },
          "price_range" : {
            "type" : "string",
            "example" : "$"
          },
          "restaurant_hours" : {
            "type" : "string"
          },
          "restaurant_id" : {
            "type" : "number",
            "example" : 396171
          },
          "restaurant_name" : {
            "type" : "string",
            "example" : "Five Brothers Kitchen and Cafe"
          },
          "restaurant_phone" : {
            "type" : "string",
            "example" : "(516) 285-0800"
          },
          "subsection" : {
            "type" : "string",
            "example" : "Beverages"
          },
          "subsection_description" : {
            "type" : "string"
          }
        }
      },
      "ResponseItem_address" : {
        "type" : "object",
        "properties" : {
          "city" : {
            "type" : "string",
            "example" : "San Francisco"
          },
          "formatted" : {
            "type" : "string",
            "example" : "43 Sutter St San Francisco, CA 94104"
          },
          "postal_code" : {
            "type" : "string",
            "example" : "94104"
          },
          "state" : {
            "type" : "string",
            "example" : "CA"
          },
          "street" : {
            "type" : "string",
            "example" : "43 Sutter St"
          }
        }
      },
      "ResponseItem_geo" : {
        "type" : "object",
        "properties" : {
          "lat" : {
            "type" : "number",
            "example" : 37.790151
          },
          "lon" : {
            "type" : "number",
            "example" : -122.401196
          }
        }
      },
      "ResponseItem_menu_item_pricing" : {
        "type" : "object",
        "properties" : {
          "currency" : {
            "type" : "string",
            "example" : "USD"
          },
          "price" : {
            "type" : "number",
            "example" : 12
          },
          "priceString" : {
            "type" : "string",
            "example" : "$12.00"
          }
        }
      },
      "ResponseRest_restaurant_address" : {
        "type" : "object",
        "properties" : {
          "city" : {
            "type" : "string",
            "example" : "CA"
          },
          "formatted" : {
            "type" : "string",
            "example" : "39 Pier Ste 255 San Francisco, CA 94133"
          },
          "postal_code" : {
            "type" : "string",
            "example" : "94133"
          },
          "state" : {
            "type" : "string",
            "example" : "San Francisco"
          },
          "street" : {
            "type" : "string",
            "example" : "39 Pier Ste 255"
          }
        }
      },
      "ResponseRest_restaurant_geo" : {
        "type" : "object",
        "properties" : {
          "lat" : {
            "type" : "number",
            "example" : 37.808674
          },
          "lon" : {
            "type" : "number",
            "example" : -122.409821
          }
        }
      },
      "ResponseRest_restaurant_pricing" : {
        "type" : "object",
        "properties" : {
          "currency" : {
            "type" : "string",
            "example" : "USD"
          },
          "price" : {
            "type" : "number",
            "example" : 9.95
          },
          "priceString" : {
            "type" : "string",
            "example" : "$9.95"
          }
        }
      },
      "ResponseRest_restaurant_menu_items" : {
        "type" : "object",
        "properties" : {
          "description" : {
            "type" : "string",
            "example" : "A nice big bowl of guacamole made table side with fresh avocados."
          },
          "name" : {
            "type" : "string",
            "example" : "Guacamole Live"
          },
          "price" : {
            "type" : "number",
            "example" : 9.95
          },
          "pricing" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/ResponseRest_restaurant_pricing"
            }
          }
        }
      },
      "ResponseRest_restaurant_menu_sections" : {
        "type" : "object",
        "properties" : {
          "description" : {
            "type" : "string",
            "example" : "Antojitos"
          },
          "menu_items" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/ResponseRest_restaurant_menu_items"
            }
          },
          "position" : {
            "type" : "number",
            "example" : 0
          },
          "section_name" : {
            "type" : "string",
            "example" : "Antojitos"
          }
        }
      },
      "ResponseRest_restaurant_menus" : {
        "type" : "object",
        "properties" : {
          "menu_name" : {
            "type" : "string",
            "example" : "Main"
          },
          "menu_sections" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/ResponseRest_restaurant_menu_sections"
            }
          }
        }
      },
      "ResponseRest_restaurant" : {
        "type" : "object",
        "properties" : {
          "address" : {
            "$ref" : "#/components/schemas/ResponseRest_restaurant_address"
          },
          "cuisines" : {
            "type" : "array",
            "example" : [ "Mexican" ],
            "items" : {
              "type" : "string"
            }
          },
          "geo" : {
            "$ref" : "#/components/schemas/ResponseRest_restaurant_geo"
          },
          "hours" : {
            "type" : "string"
          },
          "menu_tags" : {
            "type" : "array",
            "example" : [ "Antojitos", "Soups and Salads", "Fajiats Tijuana", "Taqueria", "Taqueria a la Carte", "Platos", "Kid's Corner" ],
            "items" : {
              "type" : "string"
            }
          },
          "menus" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/ResponseRest_restaurant_menus"
            }
          },
          "price_range" : {
            "type" : "string",
            "example" : "$$"
          },
          "restaurant_id" : {
            "type" : "number",
            "example" : 317120
          },
          "restaurant_name" : {
            "type" : "string",
            "example" : "Mango's"
          },
          "restaurant_phone" : {
            "type" : "string",
            "example" : "(415) 434-5000"
          }
        }
      }
    },
    "securitySchemes" : {
      "bearerAuth" : {
        "type" : "http",
        "scheme" : "bearer",
        "bearerFormat" : "JWT"
      },
      "ApiKeyAuth" : {
        "type" : "apiKey",
        "name" : "X-API-Key",
        "in" : "header"
      }
    }
  }
}
