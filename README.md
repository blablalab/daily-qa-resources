ℹ️ Repository exposing **public** links &amp; resources to the "BBC Daily" testers.

<!-- Remember that blank lines are needed before/after a section of markdown that is within an html tag, otherwise the markdown won't work -->

## Settings

#### Carpool report

```
blablacardaily://carpool_report
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://carpool_report)

#### Benefits

```
blablacardaily://benefits
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://benefits)

#### Referral

```
blablacardaily://referral?code=H2VZAN
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://referral?code=H2VZAN)

#### Statistics

```
blablacardaily://statistics?tab=current_year&auto_share=true
```

- [🔗 With `blablacardaily://` scheme (default)](blablacardaily://statistics)
- [🔗 Tab: All Time](blablacardaily://statistics?tab=all_time)
- [🔗 Tab: Current Month](blablacardaily://statistics?tab=current_month)
- [🔗 Tab: Current Year](blablacardaily://statistics?tab=current_year)
- [🔗 Tab: Current Year & Auto-Share](blablacardaily://statistics?tab=current_year&auto_share=true)

#### Communication preferences

```
blablacardaily://communication_preferences
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://communication_preferences)


##### Push

```
blablacardaily://communication_preferences?channel=PUSH
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://communication_preferences?channel=PUSH)

##### Email

```
blablacardaily://communication_preferences?channel=EMAIL
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://communication_preferences?channel=EMAIL)

##### SMS

```
blablacardaily://communication_preferences?channel=SMS
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://communication_preferences?channel=SMS)

##### Calls

```
blablacardaily://communication_preferences?channel=CALL
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://communication_preferences?channel=CALL)

##### Performance measurement

```
blablacardaily://communication_preferences?channel=PERFORMANCE_MEASUREMENT
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://communication_preferences?channel=PERFORMANCE_MEASUREMENT)

## Company (B2B)

#### Affiliation

```
blablacardaily://company_affiliation
  ?company_id=ebf1901c-290a-41b1-8edf-33ac9ed36b6c
  &affiliation_code=topSecret
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://company_affiliation?company_id=ebf1901c-290a-41b1-8edf-33ac9ed36b6c&affiliation_code=topSecret)


## Sponsor (B2G)

#### Affiliation

```
blablacardaily://sponsor_affiliation
  ?sponsor_uuid=545e51f7-741d-4522-bd07-b010be2c34ef
  &affiliation_code=s8f4o036a2dv
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://sponsor_affiliation?sponsor_uuid=545e51f7-741d-4522-bd07-b010be2c34ef&affiliation_code=s8f4o036a2dv)
- [🔗 Wrapped in **staging** Adjust link](https://l6v5.adj.st/openapp?adjust_t=1hskawr2&adjust_deeplink=blablacardaily%3A%2F%2Fsponsor_affiliation%3Fsponsor_uuid%3D545e51f7-741d-4522-bd07-b010be2c34ef%26affiliation_code%3Ds8f4o036a2dv&adjust_fallback=https%3A%2F%2Fblablacardaily.com&adj_redirect_macos=https%3A%2F%2Fblablacardaily.com)
- [🔗 Affiliation code `zvtc14d8ipwd`](blablacardaily://sponsor_affiliation?sponsor_uuid=545e51f7-741d-4522-bd07-b010be2c34ef&affiliation_code=zvtc14d8ipwd)
- [🔗 Affiliation code `lsghap9rn718`](blablacardaily://sponsor_affiliation?sponsor_uuid=545e51f7-741d-4522-bd07-b010be2c34ef&affiliation_code=lsghap9rn718)
- [Another sponsor](blablacardaily://sponsor_affiliation?sponsor_uuid=fea00ef7-9bdc-401d-8483-480dd2a437a9&affiliation_code=UJ1ie_z3ZQAJbMtZ5DFnjxY7dTzA1aeesNJg9zKf7Kw)

## Carpooling Lines

### Passenger scanning a stop pole QR code
```
blablacardaily://carpooling_lines
  ?stop_id=ebcf2f16-5362-49f6-9760-187788333e6b
```

<details>
  <summary>SQL computing markdown for a given line (run it <a href="https://redash.preprod-1.blbl.cr/queries/new">here</a>)</summary>

  ```sql
  (
      SELECT '| 🚏 Stop | 🧭 Direction | 🔗 Link |' as markdown_table_header
  )
  UNION ALL
  (
      SELECT '|:-------:|:------------:|:-------:|' as markdown_table_header_separator
  )
  UNION ALL
  (
      SELECT
          ' | '
            || substr(mp.name, length('Arrêt | '))
            || ' | '
            || (CASE 
              WHEN stop.direction = 'FORWARD' THEN 'Carcassonne'
              WHEN stop.direction = 'BACKWARD' THEN 'Pépieux'
              ELSE 'Carcassonne + Pépieux' END
            )
            || ' | '
            || '[`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=' || stop.uuid || ')'
            || ' | ' as markdown_table_entry
      FROM
          carpooling_line_stop stop
          INNER JOIN meeting_point mp ON mp.uuid = stop.meeting_point_uuid
      WHERE
          stop.carpooling_line_uuid = (
              SELECT uuid FROM carpooling_line WHERE name = 'Pépieux - Carcassonne'
          )
      ORDER BY
          stop.order ASC
  )
  ```
</details>

#### Line "Carcassonne - Pépieux" (real line)

|               🚏 Stop                |     🧭 Direction      |                                                   🔗 Link                                                    |
| :----------------------------------: | :-------------------: | :----------------------------------------------------------------------------------------------------------: |
|               Pépieux                | Carcassonne + Pépieux | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=c27e5d31-c84d-4b0a-8325-b0c9c1c96447) |
|                Azille                |      Carcassonne      | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=1666dea9-d189-49ab-9584-3799a321af0d) |
|     Rieux-Minervois - Eglantine      |      Carcassonne      | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=34438db7-a2d4-4c98-aeb4-ac464aff69e7) |
|      Rieux-Minervois - Bleuets       |      Carcassonne      | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=8a693ec2-7db4-400e-869b-f436fcc512ab) |
|      Rieux-Minervois - Bleuets       |        Pépieux        | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=9c5f488c-e2a0-46e3-8df1-05b557e0787a) |
|          Peyriac-Minervois           |      Carcassonne      | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=ad18b36b-7ed1-4ab2-9b7b-fdf25aa1cba7) |
|          Peyriac-Minervois           |        Pépieux        | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=11a331f1-088c-42c9-be03-9504518d0718) |
|               Villegly               |      Carcassonne      | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=7395238e-c6ce-47b7-9206-e3cc6d2a3fac) |
|               Villegly               |        Pépieux        | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=3c627083-67b8-4f56-8420-9d4b47e572da) |
|              Villalier               |      Carcassonne      | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=ad9942ad-8d73-4976-8d5e-866f39d8c3a4) |
|              Villalier               |        Pépieux        | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=b888fc90-0d2f-41f6-9e9b-bc5a3c37a1f7) |
|            ZA Pont Rouge             |        Pépieux        | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=9ffb87a8-24b8-45d4-b43c-d18f157ba635) |
| Carcassonne - Gare routière Varsovie | Carcassonne + Pépieux | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=64b0add0-42cb-41ed-bfda-58276ef36467) |


#### Line "Thonon - Veigy" (real line)

|      🚏 Stop        |       🧭 Direction         |                                                   🔗 Link                                                    |
|:-------------------:|:--------------------------:|:------------------------------------------------------------------------------------------------------------:|
| Thonon-les-Bains - Jules Ferry | Veigy-Foncenex | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=a8766966-ed03-4380-bd25-b7d84142fcaa) |
| Thonon-les-Bains - Létroz | Thonon-les-Bains & Veigy-Foncenex | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=573f79d3-5c69-4611-be01-938bf09dc516) |
|   Croisée d’Anthy   | Thonon-les-Bains & Veigy-Foncenex | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=0a5f2411-5140-4adb-9ba9-89dd8f180bf8) |
| Anthy-sur-Léman - Cinq Chemins | Thonon-les-Bains & Veigy-Foncenex | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=e145776a-546f-440c-a76a-f23344447b22) |
|    Sciez - Mairie   | Thonon-les-Bains & Veigy-Foncenex | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=38b90715-7594-4c77-a7b3-32453975bc27) |
|  Massongy - Centre  | Thonon-les-Bains & Veigy-Foncenex | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=38023eb1-cf39-4530-8150-9c6539f8270e) |
| Douvaine - Champ de place | Thonon-les-Bains & Veigy-Foncenex | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=d248ac9e-98aa-4f49-868c-7d8faa5b5e6a) |
|  Douvaine - Église  | Thonon-les-Bains & Veigy-Foncenex | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=0749f2df-14ba-4e19-8272-0cf750b68ef7) |
| Veigy-Foncenex - Golf | Thonon-les-Bains & Veigy-Foncenex | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=c0521347-6d8c-456a-87f4-79510f2c1a8c) |
| Veigy-Foncenex - Douane |      Thonon-les-Bains      | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=2ca2e7c8-db8f-4875-9cab-e244ac16e8ea) |


#### ~Line "Bastille - Javel"~ (fake line)

|      🚏 Stop        |       🧭 Direction         |                                                   🔗 Link                                                    |
|:-------------------:|:--------------------------:|:------------------------------------------------------------------------------------------------------------:|
|      Bastille       |           Javel            | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=c9086022-0d2e-4f6d-a200-3b7fb7e43f3e) |
|   Musée du Louvre   |      Bastille & Javel      | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=52d4790a-917e-40cf-9773-a2e807e570fb) |
| Hôtel des Invalides |           Javel            | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=e15f1abf-daa0-4911-8405-0b04a841bc6a) |
| Hôtel des Invalides |          Bastille          | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=39db1f5c-0b5a-4615-b8ca-663520cf63b4) |
|     Tour Eiffel     |           Javel            | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=9310c4eb-7800-4faf-8855-f6460ad88647) |
|     Tour Eiffel     |          Bastille          | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=a4f2f944-4dc2-4aa0-bbb7-98fc285aa40f) |
|        Javel        |          Bastille          | [`blablacardaily://` scheme](blablacardaily://carpooling_lines?stop_id=58a5da08-61a3-4191-aece-680a71c2d9af) |


### Driver scanning a passenger QR code
```
blablacardaily://carpooling_lines
  ?line_publish_id=9e865165-6616-45b1-b588-a352ce5892e1
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://carpooling_lines?line_publish_id=557515b6-b818-4952-ad1f-fc8ffeafcd09)

## Klaxit

#### Sign Up

```
blablacardaily://klaxit_sign_up
  ?first_name=Pierre%20Olivier
  &picture_url=https%3A%2F%2Fklaxit.com%2Fpicture%2Fuser42.png
```

- [🔗 With `blablacardaily://` scheme](blablacardaily://klaxit_sign_up?first_name=Klaxit&picture_url=https%3A%2F%2Fdxxbxu0f802py.cloudfront.net%2Fwp-content%2Fuploads%2F2023%2F03%2F14100407%2F03.png)


## IDFM Partner

#### IDFMConnect Accounts Management

- [🔗 Integration](https://int-connect.navigo.fr/auth/realms/connect/protocol/openid-connect/auth?client_id=account) (used by Daily staging)
- [🔗 Production](https://connect.navigo.fr/auth/realms/connect/protocol/openid-connect/auth?client_id=account) (used by Daily production)

#### Search on IDFM
```
blablacardaily://search
  ?departure_location=lat%3D48.803890%2Clon%3D2.126782
  &arrival_location=lat%3D48.869384%2Clon%3D2.337933
  &departure_datetime=2021-08-23T08%3A00%3A00%2B01%3A00
  &partner=NAVIGO
  &utm_campaign=FR_NAT_PARTNERS
```
- [🔗 With `blablacardaily://` scheme](blablacardaily://search?departure_location=lat%3D48.803890%2Clon%3D2.126782&arrival_location=lat%3D48.869384%2Clon%3D2.337933&departure_datetime=2021-08-23T08%3A00%3A00%2B01%3A00&partner=NAVIGO&utm_campaign=FR_NAT_PARTNERS)

## Google Maps Partner

#### Search with pickup=`my_location` & drop-off in IDF
```
// "My location" -> "Château de Versailles"
blablacardaily://book-a-ride
  ?pickup=my_location
  &dropoff_latitude=48.803890
  &dropoff_longitude=2.126782
```
- [🔗 With `blablacardaily://` scheme](blablacardaily://book-a-ride?pickup=my_location&dropoff_latitude=48.803890&dropoff_longitude=2.126782)
- [🔗 With `https://` scheme](https://open.blablacardaily.com/book-a-ride?pickup=my_location&dropoff_latitude=48.803890&dropoff_longitude=2.126782)

#### Search with pickup in IDF & drop-off=`my_location`
```
// "Château de Versailles" -> "My location"
blablacardaily://book-a-ride
  ?dropoff=my_location
  &pickup_latitude=48.803890
  &pickup_longitude=2.126782
```
- [🔗 With `blablacardaily://` scheme](blablacardaily://book-a-ride?dropoff=my_location&pickup_latitude=48.803890&pickup_longitude=2.126782)
- [🔗 With `https://` scheme](https://open.blablacardaily.com/book-a-ride?dropoff=my_location&pickup_latitude=48.803890&pickup_longitude=2.126782)

#### Search with pickup & drop-off in IDF
```
// "6, rue Saint-Sabin" -> "Château de Versailles"
blablacardaily://book-a-ride
  ?pickup_latitude=48.85504296738133
  &pickup_longitude=2.3719849244470934
  &dropoff_latitude=48.803890
  &dropoff_longitude=2.126782
```
- [🔗 With `blablacardaily://` scheme](blablacardaily://book-a-ride?pickup_latitude=48.85504296738133&pickup_longitude=2.3719849244470934&dropoff_latitude=48.803890&dropoff_longitude=2.126782)
- [🔗 With `https://` scheme](https://open.blablacardaily.com/book-a-ride?pickup_latitude=48.85504296738133&pickup_longitude=2.3719849244470934&dropoff_latitude=48.803890&dropoff_longitude=2.126782)

#### Search with pickup=`my_location` & drop-off *not* in IDF
```
// "My location" -> "Parlement de Bretagne (Rennes)"
blablacardaily://book-a-ride
  ?pickup=my_location
  &dropoff_latitude=48.11177009606368
  &dropoff_longitude=-1.6775474034472833
```
- [🔗 With `blablacardaily://` scheme](blablacardaily://book-a-ride?pickup=my_location&dropoff_latitude=48.11177009606368&dropoff_longitude=-1.6775474034472833)
- [🔗 With `https://` scheme](https://open.blablacardaily.com/book-a-ride?pickup=my_location&dropoff_latitude=48.11177009606368&dropoff_longitude=-1.6775474034472833)

## Adjust links

### Staging (`l6v5.adj.st`)

- [Adjust tracker `14wcmffh` (QuickStart New Members)](https://l6v5.adj.st/openapp?adjust_t=14wcmffh&adjust_deeplink=blablacardaily%3A%2F%2Fhome%3Forigin%3DQUICKSTART_NEW_MEMBER&adjust_fallback=https%3A%2F%2Fblablacardaily.com)
- [Adjust tracker `1hskawr2` (Company Affiliation) n°1](https://l6v5.adj.st/openapp?adjust_t=1hskawr2&adjust_deeplink=blablacardaily%3A%2F%2Fcompany_affiliation%3Fcompany_uuid%3D6fe0c6a8-049d-4030-8ced-64cf3c452c49%26affiliation_code%3DiKZ704BaM937vFqiQN2juVdxQXFnlEGTDRqy0ARPhZk&adjust_fallback=https%3A%2F%2Fblablacardaily.com&adj_redirect_macos=https%3A%2F%2Fblablacardaily.com)
- [Adjust tracker `1hskawr2` (Company Affiliation) n°2](https://l6v5.adj.st/openapp?adjust_t=1hskawr2&adjust_deeplink=blablacardaily%3A%2F%2Fhome&adjust_fallback=https%3A%2F%2Fblablacardaily.com&adj_redirect_macos=https%3A%2F%2Fblablacardaily.com)
- [CarpoolingLines - wrong tracker](https://l6v5.adj.st/openapp?adjust_t=1hskawr2&adjust_deeplink=blablacardaily%3A%2F%2Fcarpooling_lines%3Fstop_id%3D8975bbd1-0b20-4fc8-a4ef-31818e73f37f&adjust_fallback=https%3A%2F%2Fblablacardaily.com)

### Production (`dfj5.adj.st`)

- TODO
