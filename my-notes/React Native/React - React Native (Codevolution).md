Codevolution - https://www.youtube.com/watch?v=hzzCveeczSQ&list=PLC3y8-rFHvwhiQJD1di4eRVN30WWCXkg1&ab_channel=Codevolution

![[Pasted image 20240503151933.png]]![[Pasted image 20240503165632.png]]
![[Pasted image 20240503171055.png]]
IOS apps requires Swift of Objective-C
Android apps requires Java or Kotlin
React Native apps works seamlessly on both platforms

npx create-expo-app@lastest HelloWorld

## CORE COMPONENTS
![[Pasted image 20240504165830.png]]

## VIEW
![[Pasted image 20240504170156.png]]
![[Pasted image 20240504171338.png]]

## Text
![[Pasted image 20240504171434.png]]
![[Pasted image 20240504172355.png]]

## IMAGE
![[Pasted image 20240504173702.png]]
![[Pasted image 20240504173803.png]]![[Pasted image 20240504174127.png]]
![[Pasted image 20240507030626.png]]
Image sizing
![[Pasted image 20240507030848.png]]

## SCROLL VIEW
![[Pasted image 20240504174525.png]]
![[Pasted image 20240504174714.png]]

## BUTTON
![[Pasted image 20240504175127.png]]
![[Pasted image 20240504180012.png]]

## PRESSABLE
![[Pasted image 20240504180536.png]]
![[Pasted image 20240504180556.png]]

## MODAL
![[Pasted image 20240504180715.png]]![[Pasted image 20240504181123.png]]
![[Pasted image 20240504181329.png]]
presentationStyle is an IOS exclusive attribute

## STATUS BAR
![[Pasted image 20240506170727.png]]
![[Pasted image 20240506170708.png]]
![[Pasted image 20240507031830.png]]


## ACTIVITY INDICATOR
![[Pasted image 20240506170800.png]]
![[Pasted image 20240506170955.png]]
animating constrols visibility

## ALERT
![[Pasted image 20240506182220.png]]
![[Pasted image 20240506182202.png]]

## CUSTOM COMPONENTS
![[Pasted image 20240506182519.png]]

## STYLING REACT NATIVE APPS
![[Pasted image 20240506182644.png]]
![[Pasted image 20240506182730.png]]

## STYLESHEET API
![[Pasted image 20240506203849.png]]

## MULTIPLE STYLES
 ![[Pasted image 20240506204301.png]]
IOS : Border radius works only on View component
Android : Border radius works on both View and Text components

## BOX SHADOW
![[Pasted image 20240506210033.png]]
On Android you have to use the elevation property
The only property ios and android share is shadowColor


## STYLE INHERITANCE
![[Pasted image 20240506230241.png]]
Components dont' have inheritance; React Native only supports inheritance between `Text` components

## EXTEND STYLES
![[Pasted image 20240506232055.png]]
In the parent component, you can specify extended styles and the content of the box through props

## FLEX
![[Pasted image 20240506232629.png]]
The view component is always a flex box cointainer by default

![[Pasted image 20240506233132.png]]
Box 2 takes tree times Box 1 space available

## ALIGN ITEMS
align items baseline
![[Pasted image 20240506233753.png]]

## ALIGN SELF
Item property
Aligns items itself in the cross axis
![[Pasted image 20240506234258.png]]
If align items is auto, the component takes the property values of the parent

## ALIGN CONTENT
![[Pasted image 20240506234731.png]]
![[Pasted image 20240506234739.png]]

## GAP
![[Pasted image 20240506234917.png]]

## FLEX BASIS
![[Pasted image 20240506235003.png]]
![[Pasted image 20240506235236.png]]
flex grow space distribution its only compatible with flex basis property

## FLEX SHRINK
![[Pasted image 20240506235537.png]]
Box 2 will shrink to fit the container and shrinks its content

## FLEX GROW
![[Pasted image 20240507000019.png]]

## DIMENSIONS API
```jsx
import {Dimensions} from 'react-native'
```
![[Pasted image 20240507001132.png]]

## DIMENSIONS API DRAWBACK
Dimesions API doesn't detect orientation changes
Establish a subscription to monitor orientation changes and apply the necessary modifications
![[Pasted image 20240507001436.png]]
![[Pasted image 20240507002009.png]]

## USE WINDOW DIMENSIONS
useWindowDimensions detect orientation changes
![[Pasted image 20240507002339.png]]

## SAFE AREA VIEW
![[Pasted image 20240507003138.png]]
![[Pasted image 20240507003152.png]]

## PLATFORM SPECIFIC CODE
![[Pasted image 20240507003224.png]]
![[Pasted image 20240507003342.png]]

Select OS specific styles
![[Pasted image 20240507003500.png]]

Platform specific extensions
![[Pasted image 20240507003703.png]]
![[Pasted image 20240507003725.png]]
React Native renders the corresponding components related to the current operating system (OS)

## LISTS
![[Pasted image 20240507031649.png]]
not recommended
![[Pasted image 20240507032120.png]]

## FLATLIST
![[Pasted image 20240507032214.png]]
![[Pasted image 20240507032318.png]]
horizontal prop
```html
<FlatList horizontal={true} />
<FlatList horizontal />
```
keyExtractor prop
```html
<FlatList keyExtractor={(item, index) => item.id.toString()}/>
<FlatList horizontal />
```
ItemSeparatorComponet prop
```jsx
<Flatlist
	ItemSeparatorComponent={<View style={{height: 16}}/>}
/>
```
ListEmptyComponent
```jsx
<Flatlist
	ListEmptyComponent={<Text>No items found</Text>}
/>
```
ListHeaderComponent prop
```jsx
<Flatlist
	ListHeaderComponent={<Text>Header</Text>}
/>
```
ListFooterComponent
```jsx
<Flatlist
	ListFooterComponent={<Text>Footer</Text>}
/>
```

## SECTION LIST
![[Pasted image 20240507033401.png]]
![[Pasted image 20240507033806.png]]
```jsx
<SectionList
        sections={groupedPokemonList}
        renderItem={({ item }) => {
          return (
            <View style={styles.card}>
              <Text style={styles.cardText}>{item}</Text>
            </View>
          );
        }}
        renderSectionHeader={({ section }) => (
          <Text style={styles.sectionHeaderText}>{section.type}</Text>
        )}
        ItemSeparatorComponent={() => (
          <View
            style={{
              height: 16,
            }}
          />
        )}
        SectionSeparatorComponent={() => (
          <View
            style={{
              height: 16,
            }}
          />
        )}
    />
```

## FORMS
![[Pasted image 20240507164416.png]]![[Pasted image 20240507164513.png]]


## TEXT INPUT
![[Pasted image 20240509020646.png]]
The text input component doesn't have styles by default
![[Pasted image 20240509021128.png]]

## TEXT INPUT PROPS
placeholder
secure text entry (boolean)
keyboard type (string)
autocorrect (true by default)
autocapitalize (string) (characters - none - sentences - words)

MULTILINE TEXT INPUT
![[Pasted image 20240509021715.png]]
add | textAlignVertical: 'top' | to adjust android text alignment, no such problem appears on IOS

## SWITCH
![[Pasted image 20240509022653.png]]
![[Pasted image 20240509022911.png]]

## KEYBOARD AVOIDING VIEW
![[Pasted image 20240509031606.png]]

## FORM VALIDATION
![[Pasted image 20240509114332.png]]

## GET REQUESTS
![[Pasted image 20240509163812.png]]

## PULL TO REFRESH
![[Pasted image 20240509164436.png]]
refreshing prop in FlatList component
![[Pasted image 20240509164510.png]] 
![[Pasted image 20240509164613.png]]

POST REQUEST
![[Pasted image 20240509165455.png]]
![[Pasted image 20240509165428.png]]

## NAVIGATION
![[Pasted image 20240509173525.png]]
![[Pasted image 20240509173711.png]]
https://reactnavigation.org/
![[Pasted image 20240509173846.png]]

## STACK NAVIGATION
![[Pasted image 20240509220327.png]]

![[Pasted image 20240509220428.png]]
Documentation
```jsx
import { createNativeStackNavigator } from '@react-navigation/native-stack';  
  
const Stack = createNativeStackNavigator();  
  
function MyStack() {  
	return (  
		<Stack.Navigator>  
			<Stack.Screen name="Home" component={Home} />  
			<Stack.Screen name="Notifications" component={Notifications} />  
			<Stack.Screen name="Profile" component={Profile} />  
			<Stack.Screen name="Settings" component={Settings} />  
		</Stack.Navigator>  
	);  
}
```
Course
![[Pasted image 20240509221215.png]]

## NAVIGATION BETWEEN SCREENS
two similar ways
![[Pasted image 20240509221943.png]]
every screen component receives the navigation prop by default

useNavigation hook
![[Pasted image 20240509222234.png]]

- Navigation Prop : available only in screen components, use it all as you can
- Navigation Hook : available in the entire app, needs to write an import

## PASSING DATA BETWEEN SCREENS
pass data from navigation
![[Pasted image 20240509223232.png]]
destructure param
![[Pasted image 20240509223248.png]]
initial value param
![[Pasted image 20240509223308.png]]
update param (set params)
![[Pasted image 20240509223404.png]]

## STACK NAVIGATION OPTIONS
![[Pasted image 20240509224456.png]]

options also can be configured on screen component
![[Pasted image 20240509224607.png]]

## DYNAMIC STACK NAVIGATOR OPTIONS
title
![[Pasted image 20240510004852.png]]
![[Pasted image 20240510004918.png]]

dynamic title ( setOptions )
![[Pasted image 20240510005122.png]]

## DRAWER NAVIGATION
https://www.reanimated2.com/docs/fundamentals/getting-started
![[Pasted image 20240510010540.png]]
![[Pasted image 20240510010523.png]]

## DRAWER NAVIGATION OPTIONS
![[Pasted image 20240510010840.png]]

## BOTTOM TABS NAVIGATOR
https://reactnavigation.org/docs/bottom-tab-navigator
![[Pasted image 20240510011105.png]]

## BOTTOM TABS NAVIGATOR OPTIONS
- label position
- show label
- active tab tint color
- inactive tint color
- tab bar label
- tab bar icon ( use ionIcons of expo )
- tab bar badge ( notifications )

## NESTING NAVIGATORS
![[Pasted image 20240510011824.png]]
![[Pasted image 20240510012342.png]]
AboutStack is an Stack wrapped on a NavigationContainer component



![[Pasted image 20240527131118.png]]
adaptiveicon :  es el iconito que se muestra en el menu de aplicaciones del smartphone
favicon : me parece que es de web, no es tan importante
icon : no sabemos bien que es, tratá de que coincida con el circulito
logo : logo que se muestra en la barra superior
splash : logo que se muestra cuando abris la aplicacion y esta cargando