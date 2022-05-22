<template>
  <v-container fluid class="blue lighten-4 ml-6" style="width: 96vw">
	<v-layout row wrap>
		<v-flex xs12 sm6 md4 lg3 v-for="(item, index) in workerList" :key="item">
		<v-card :loading="loading" height="auto" class="ma-4 pa-3" elevation="5">
			<v-container>
				<v-col>
					<v-col>
						<v-row class="mb-2">
							<v-spacer></v-spacer>
								<v-menu
									offset-y
									bottom
									:close-on-click="closeOnClick"
									>
									<template v-slot:activator="{ on, attrs }">
										<v-btn
										color="indigo accent-4"
										dark
										v-bind="attrs"
										v-on="on"
										>
										<v-icon>mdi-menu</v-icon>
										</v-btn>
									</template>

									<v-list>
										<template v-if="workerList[index].isActive == true">
										<v-list-item @click="workerList[index].isActive = false">Deactivate</v-list-item>
										</template>
										<template v-if="workerList[index].isActive == false">
										<v-list-item @click="workerList[index].isActive = true">Activate</v-list-item>
										</template>
										<v-list-item @click="workerList.splice(index,1)">Delete user</v-list-item>
									</v-list>
								</v-menu>
						</v-row>
					</v-col>
				
				</v-col>
				<v-row>
					<v-row>
					<v-avatar size="120" class="blue ml-7">
						<v-img
						:src="workerList[index].picture.medium"
						alt="user photo"
						contain
						></v-img>
					</v-avatar>
						<v-col class="ml-4" style="opacity: .9">
							<v-row class="align-center">
								<template v-if="workerList[index].isActive == true"><v-icon color="green">
									mdi-account-check
									</v-icon>
								</template>
								<template v-if="workerList[index].isActive == false"><v-icon color="purple">
									mdi-account-remove
									</v-icon>
								</template>
								<p class="indigo--text text-subtitle-2 ml-1 mb-0">
									{{workerList[index].isActive ? "active" : "inactive"}}
								</p>
							</v-row>
							<v-row class="align-center">
								<v-icon color="indigo">mdi-calendar-plus</v-icon>
								<p class="indigo--text text-subtitle-2 ml-1 mb-0">
									{{workerList[index].registered.slice(0,10)}}
								</p>
							</v-row>
							<v-row class="align-center">
								<v-icon color="indigo">mdi-calendar-clock</v-icon>
								<p class="indigo--text text-subtitle-2 ml-1 mb-0">
									{{workerList[index].registered.slice(11,19)}}
								</p>
							</v-row>
							<v-row class="align-center">
								<v-icon color="indigo">mdi-flag</v-icon>
								<p class="indigo--text text-subtitle-2 ml-1 mb-0">
								{{workerList[index].nationality}}
								</p>
							</v-row>
							<v-row class="align-center">
									<template v-if="workerList[index].gender == 'male'">
									<v-icon color="indigo">mdi-gender-male</v-icon>
									<p class="indigo--text text-subtitle-2 ml-1 mb-0">
									male</p>
									</template>
									<template v-if="workerList[index].gender == 'female'">
									<v-icon color="indigo">mdi-gender-female</v-icon>
									<p class="indigo--text text-subtitle-2 ml-1 mb-0">
									female</p>
									</template>
							</v-row>
						</v-col>
					</v-row>
				</v-row>
				<v-row>
					<v-card-title class="mt-3">
						<h2 class="indigo--text">{{workerList[index].name.first}} {{workerList[index].name.last}}</h2>

					</v-card-title>
				</v-row>
				<v-col class="pa-5 ml-0">
					<v-row>
						<v-icon color="indigo lighten-1" left>mdi-email</v-icon>
						<span class="indigo--text">{{workerList[index].email}}</span>
					</v-row>
					<v-row>
						<v-icon color="indigo lighten-1" left>mdi-phone</v-icon>
						<span class="indigo--text">{{workerList[index].phone}}</span>
					</v-row>
					<v-row>
						<v-icon color="indigo lighten-1" left>mdi-cellphone</v-icon>
						<span class="indigo--text">{{workerList[index].cell}}</span>
					</v-row>
				</v-col>
				<v-col class="blue lighten-5 pa-5 mt-6 rounded-lg">
					<v-row>
						<v-icon color="indigo lighten-1" left>mdi-map-marker-radius</v-icon>
						<span class="indigo--text"><b>Location</b></span>
					</v-row>

					<div class="mt-5 mb-6 ml-1">
					<v-row>
						<span class="indigo--text"><b>Street: </b>{{workerList[index].location.street.number}} {{workerList[index].location.street.name}}</span>
					</v-row>
					<v-row>
						<span class="indigo--text"><b>State: </b>{{workerList[index].location.state}}</span>
					</v-row>
					<v-row>
						<span class="indigo--text"><b>City: </b>{{workerList[index].location.city}}</span>
						</v-row>
					<v-row>
						<span class="indigo--text"><b>Postcode: </b>{{workerList[index].location.postcode}}</span>
						</v-row>
					<v-row>
						<span class="indigo--text"><b>Country: </b>{{workerList[index].location.country}}</span>
						</v-row>
					</div>
					<v-btn color="blue lighten-2" dark style="margin-left: -8px"
						:href="`https://www.google.com/maps/@${workerList[index].location.coordinates.latitude},${workerList[index].location.coordinates.longitude},8z`"
						target="_blank">
					<span>Map</span>
					</v-btn>
				</v-col>

				<v-card-actions class="pl-3 pt-5 pb-5 mt-8" style="border-radius: 8px;">
					<v-menu 
						offset-y
						bottom
						:close-on-click="closeOnClick"
						>
						<template v-slot:activator="{ on, attrs }">
							<v-btn
							color="blue darken-2"
							dark
							v-bind="attrs"
							v-on="on"
							>
							Message
							</v-btn>
						</template>
						<v-list>
							<v-list-item 
							:href="`mailto:${workerList[index].email}`"
							target="_blank">
							<span>Email</span>
						</v-list-item>
						<v-list-item>
							<span class="grey--text">WhatsApp</span> 
						</v-list-item>
						<v-list-item>
							<span class="grey--text">Telegram</span>
						</v-list-item>
						</v-list>
						</v-menu>
					<v-btn color="blue darken-2" dark class="ml-2">Call</v-btn>
				</v-card-actions>
			</v-container>
		</v-card>
		</v-flex>

	<!-- add user -->
		<v-flex xs12 sm6 md4 lg3>
		<v-card :loading="loading" height="auto" class="ma-4 pa-3" elevation="5" style="outline: 2px solid grey;">
			<v-container>
				<v-col>
					<v-col>
						<v-row class="mb-2">
							<v-spacer></v-spacer>

								<v-menu
									offset-y
									bottom
									:close-on-click="closeOnClick"
								>
								<v-list>
									<template v-if="workerList[0].isActive == true">
									<v-list-item @click="workerList[0].isActive = false">Deactivate</v-list-item>
									</template>
									<template v-if="workerList[0].isActive == false">
									<v-list-item @click="workerList[0].isActive = true">Activate</v-list-item>
									</template>
									<v-list-item @click="workerList.splice(0,1)">Delete user</v-list-item>
									</v-list>
								</v-menu>
						</v-row>
					</v-col>
				
				</v-col>
				<v-row>
					<v-row>
					<v-avatar size="120" class="blue ml-7">
						<v-img
						:src="workerList[0].picture.medium"
						alt="user photo"
						contain
						></v-img>
					</v-avatar>
						<v-col class="ml-4" style="opacity: .9">
							<v-row class="align-center">
								<v-icon color="indigo">
									mdi-account-question-outline
								</v-icon>
								<p class="indigo--text text-subtitle-2 ml-1 mb-0">
									<select v-model="selected">
									<option disabled value="" class="indigo--text">Select status</option>
									<option>Active</option>
									<option>Inactive</option>
									</select>
								</p>
							</v-row>
							<v-row class="align-center">
								<v-icon color="indigo">mdi-calendar-plus</v-icon>
								<p class="indigo--text text-subtitle-2 ml-1 mb-0">
									_______
								</p>
							</v-row>
							<v-row class="align-center">
								<v-icon color="indigo">mdi-calendar-clock</v-icon>
								<p class="indigo--text text-subtitle-2 ml-1 mb-0">
									_______
								</p>
							</v-row>
							<v-row class="align-center">
								<v-icon color="indigo">mdi-flag</v-icon>
								<p class="grey--text text-subtitle-2 ml-1 mb-0">
								select nationality
								</p>
							</v-row>
							<v-row class="align-center">
									<v-icon color="indigo">mdi-gender-male-female</v-icon>
									<p class="grey--text text-subtitle-2 ml-1 mb-0">
									select gender</p>
							</v-row>
						</v-col>
					</v-row>
				</v-row>
				<v-row>
					<v-card-title class="mt-3">
						<span class="indigo--text"><input v-model="addUserName" placeholder="enter name"></span>
						<span class="indigo--text"><input v-model="addUserSurname" placeholder="enter surname"></span>
					</v-card-title>
				</v-row>
				<v-col class="pa-5 ml-0">
					<v-row>
						<v-icon color="grey" left>mdi-email</v-icon>
						<span class="indigo--text"><input v-model="addUserEmail" placeholder="enter email"></span>
					</v-row>
					<v-row>
						<v-icon color="grey" left>mdi-phone</v-icon>
						<span class="indigo--text"><input v-model="addUserPhone" placeholder="enter phone"></span>
					</v-row>
					<v-row>
						<v-icon color="grey" left>mdi-cellphone</v-icon>
						<span class="indigo--text"><input v-model="addUserCell" placeholder="enter mobile phone"></span>
					</v-row>
				</v-col>
				<v-col class="grey lighten-3 pa-5 mt-6 rounded-lg">
					<v-row>
						<v-icon color="indigo lighten-1" left>mdi-map-marker-radius</v-icon>
						<span class="indigo--text"><b>Location</b></span>
					</v-row>

					<div class="mt-5 mb-6 ml-1">
					<v-row>
						<span class="indigo--text"><v-text-field v-model="addUserStreet" placeholder="enter street"></v-text-field></span>
					</v-row>
					<v-row>
						<span class="indigo--text"><v-text-field v-model="addUserState" placeholder="enter state"></v-text-field></span>
					</v-row>
					<v-row>
						<span class="indigo--text"><v-text-field v-model="addUserCity" placeholder="enter city"></v-text-field></span>
					</v-row>
					<v-row>
						<span class="indigo--text"><v-text-field v-model="addUserPostcode" placeholder="enter postcode"></v-text-field></span></v-row>
					<v-row>
						<span class="indigo--text"><v-text-field v-model="addUserState" placeholder="enter country"></v-text-field></span>
						</v-row>
					</div>
				</v-col>

				<v-card-actions class="pl-3 pt-5 pb-5 mt-8" style="border-radius: 8px;">
					<v-btn
						color="indigo accent-4"
						dark
						>Add user
						<v-icon>mdi-plus</v-icon>
					</v-btn>
				</v-card-actions>
			</v-container>
		</v-card>
		</v-flex>
	</v-layout>
  </v-container>
</template>

<script>
  export default {
    name: 'workerList',
    data: () => ({
        workerList: [
			{
				"gender":"male",
				"name":{
					"first":"Brian",
					"last":"Adams"
				},
				"location":{
					"street":{
						"number":734,
						"name":"Park Road"
					},
					"city":"Stoke-on-Trent",
					"state":"County Fermanagh",
					"country":"United Kingdom",
					"postcode":"XR3 9EY",
					"coordinates":{
						"latitude":"18.0015",
						"longitude":"-86.0374"
					}
				},
				"email":"brian.adams@example.com",
				"registered":"2008-11-07T11:53:14.120Z",
				"phone":"015394 84142",
				"cell":"0737-492-043",
				"isActive": true,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/men/42.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/men/42.jpg"
				},
				"nationality":"GB"
			},
			{
				"gender":"female",
				"name":{
					"first":"Izzie",
					"last":"Lewis"
				},
				"location":{
					"street":{
						"number":8255,
						"name":"The Avenue"
					},
					"city":"Londonderry",
					"state":"County Antrim",
					"country":"United Kingdom",
					"postcode":"MY2L 6XU",
					"coordinates":{
						"latitude":"8.3835",
						"longitude":"-165.2342"
					}
				},
				"email":"izzie.lewis@example.com",
				"registered":"2002-11-15T03:25:56.986Z",
				"phone":"016977 4085",
				"cell":"0724-047-718",
				"isActive": true,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/women/37.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/women/37.jpg"
				},
				"nationality":"GB"
			},
			{
				"gender":"male",
				"name":{
					"first":"Cody",
					"last":"Kuhn"
				},
				"location":{
					"street":{
						"number":734,
						"name":"Park Road"
					},
					"city":"Stoke-on-Trent",
					"state":"County Fermanagh",
					"country":"United Kingdom",
					"postcode":"XR3 9EY",
					"coordinates":{
						"latitude":"18.0015",
						"longitude":"-86.0374"
					}
				},
				"email":"cody.kuhn@example.com",
				"registered":"2010-09-29T06:49:00.828Z",
				"phone":"01200 69421",
				"cell":"0783-755-349",
				"isActive": true,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/men/2.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/men/2.jpg"
				},
				"nationality":"GB"
			},
			{
				"gender":"male",
				"name":{
					"first":"Nathaniel",
					"last":"Watson"
				},
				"location":{
					"street":{
						"number":3319,
						"name":"Victoria Road"
					},
					"city":"Glasgow",
					"state":"County Tyrone",
					"country":"United Kingdom",
					"postcode":"W2 2HU",
					"coordinates":{
						"latitude":"-20.8721",
						"longitude":"-114.2121"
					}
				},
				"email":"nathaniel.watson@example.com",
				"registered":"2003-04-14T21:48:07.281Z",
				"phone":"013873 95678",
				"cell":"0730-343-076",
				"isActive": true,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/men/81.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/men/81.jpg"
				},
				"nationality":"GB"
			},
			{
				"gender":"male",
				"name":{
					"first":"Ricardo",
					"last":"Chapman"
				},
				"location":{
					"street":{
						"number":3731,
						"name":"Manchester Road"
					},
					"city":"Londonderry",
					"state":"Somerset",
					"country":"United Kingdom",
					"postcode":"O8J 4NR",
					"coordinates":{
						"latitude":"-37.1195",
						"longitude":"-78.8375"
					}
				},
				"email":"ricardo.chapman@example.com",
				"registered":"2007-01-01T17:38:32.166Z",
				"phone":"017687 58960",
				"cell":"0740-826-264",
				"isActive": true,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/men/36.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/men/36.jpg"
				},
				"nationality":"GB"
			},
			{
				"gender":"female",
				"name":{
					"first":"Patricia",
					"last":"Alexander"
				},
				"location":{
					"street":{
						"number":1138,
						"name":"Grove Road"
					},
					"city":"Liverpool",
					"state":"Dyfed",
					"country":"United Kingdom",
					"postcode":"Z15 2TT",
					"coordinates":{
						"latitude":"-34.4501",
						"longitude":"-81.7062"
					}
				},
				"email":"patricia.alexander@example.com",
				"registered":"2008-08-14T04:04:00.735Z",
				"phone":"015395 46775",
				"cell":"0775-286-928",
				"isActive": true,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/women/49.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/women/49.jpg"
				},
				"nationality":"GB"
			},
			{
				"gender":"female",
				"name":{
					"first":"Amy",
					"last":"Jackson"
				},
				"location":{
					"street":{
						"number":6268,
						"name":"Manchester Road"
					},
					"city":"Plymouth",
					"state":"North Yorkshire",
					"country":"United Kingdom",
					"postcode":"BW8 2XY",
					"coordinates":{
						"latitude":"-39.7456",
						"longitude":"0.9339"
					}
				},
				"email":"amy.jackson@example.com",
				"registered":"2012-11-10T19:53:15.592Z",
				"phone":"017687 25568",
				"cell":"0762-593-441",
				"isActive": true,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/women/39.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/women/39.jpg"
				},
				"nationality":"GB"
			},
			{
				"gender":"male",
				"name":{
					"first":"Clifton",
					"last":"Jacobs"
				},
				"location":{
					"street":{
						"number":1138,
						"name":"Grove Road"
					},
					"city":"Liverpool",
					"state":"Dyfed",
					"country":"United Kingdom",
					"postcode":"Z15 2TT",
					"coordinates":{
						"latitude":"-34.4501",
						"longitude":"-81.7062"
					}
				},
				"email":"clifton.jacobs@example.com",
				"registered":"2015-05-02T21:04:19.014Z",
				"phone":"017684 26947",
				"cell":"0705-776-434",
				"isActive": false,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/men/1.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/men/1.jpg"
				},
				"nationality":"GB"
			},
			{
				"gender":"male",
				"name":{
					"first":"Adrian",
					"last":"Hart"
				},
				"location":{
					"street":{
						"number":1138,
						"name":"Grove Road"
					},
					"city":"Liverpool",
					"state":"Dyfed",
					"country":"United Kingdom",
					"postcode":"Z15 2TT",
					"coordinates":{
						"latitude":"-34.4501",
						"longitude":"-81.7062"
					}
				},
				"email":"adrian.hart@example.com",
				"registered":"2016-07-16T19:18:19.396Z",
				"phone":"016974 64899",
				"cell":"0751-557-596",
				"isActive": false,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/men/79.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/men/79.jpg"
				},
				"nationality":"GB"
			},
			{
				"gender":"male",
				"name":{
					"first":"Ivan",
					"last":"Mitchelle"
				},
				"location":{
					"street":{
						"number":1028,
						"name":"Broadway"
					},
					"city":"Nottingham",
					"state":"County Tyrone",
					"country":"United Kingdom",
					"postcode":"P2 4TG",
					"coordinates":{
						"latitude":"17.5335",
						"longitude":"73.7684"
					}
				},
				"email":"ivan.mitchelle@example.com",
				"registered":"2017-09-15T10:11:59.248Z",
				"phone":"017683 17416",
				"cell":"0712-900-947",
				"isActive": true,
				"picture":{
					"medium":"https://randomuser.me/api/portraits/med/men/82.jpg",
					"thumbnail":"https://randomuser.me/api/portraits/thumb/men/82.jpg"
				},
				"nationality":"GB"
			}
		],
    }),

	model: null,
    
	classes: [
        ['h1', 'Heading 1', '6rem', '300', '-.015625em', -1],
        ['h2', 'Heading 2', '3.75rem', '300', '-.0083333333em', 0],
        ['h3', 'Heading 3', '3rem', '400', 'normal', 1],
        ['h4', 'Heading 4', '2.125rem', '400', '.0073529412em', 2],
        ['h5', 'Heading 5', '1.5rem', '400', 'normal', 2],
        ['h6', 'Heading 6', '1.25rem', '500', '.0125em', 3],
        ['subtitle-1', 'Subtitle 1', '1rem', '400', '.009375em', 4],
        ['subtitle-2', 'Subtitle 2', '0.875rem', '500', '.0071428571em', 4],
        ['body-1', 'Body 1', '1rem', '400', '.03125em', 4],
        ['body-2', 'Body 2', '0.875rem', '400', '.0178571429em', 4],
        ['button', 'Button', '0.875rem', '500', '.0892857143em', 4],
        ['caption', 'Caption', '0.75rem', '400', '.0333333333em', 4],
        ['overline', 'Overline', '0.75rem', '500', '.1666666667em', 4],
      ],
  }
</script>

<!-- <style scoped>
	div {
		border: 1px solid red;
	};
</style> -->