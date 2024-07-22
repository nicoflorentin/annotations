## Indice

Gibson, [6/10/2024 10:18 AM] Buen dia compañeros!, espero que hayan descansado el fin de semana, aqui les dejo una lista de temas a repasarde react native:

Componentes Específicos de React Native:

```
Componentes básicos de React Native: View, Text, Image, ScrollView, FlatList.
Diferencias entre los componentes de React (DOM) y React Native (nativos).
```

Estilos en React Native:

```
Uso de StyleSheet en lugar de CSS.
Flexbox para el diseño de interfaces (similar a web, pero con pequeñas diferencias).
```

Navegación:

```
Configuración y uso de React Navigation.
Diferentes tipos de navegadores: Stack Navigator, Tab Navigator, Drawer Navigator.
```

Acceso a APIs Nativas:

`Uso de librerías (EXPO) para acceder a funcionalidades nativas (ej. cámara, ubicación, almacenamiento) Introducción a react-native-gesture-handler y react-native-reanimated`

Manejo del Estado y Zustand:

```
Uso de useState, useEffect en React Native.
```

Uso de Zustand como gestor del estado global de una app de react native

Fetching de datos con fetch o axios. Manejo de promesas y asincronía en React Native.

pueden revisar este curso en udemy, que es gratuito (solo deben abrir una cuenta y enrolarse) : [https://www.udemy.com/course/react-native-tutorial/](https://www.udemy.com/course/react-native-tutorial/)

aqui va otro : [https://www.udemy.com/course/react-native-full-course/](https://www.udemy.com/course/react-native-full-course/)

Gibson, [6/10/2024 10:22 AM] este ultimo indica en la descripcion que usan la libreria de UI Ract native Paper pueden ponerle mas atencion a este puesto que esa libreria es la que vamos a usar para no estar creando componentes basicos como botones y eso

[https://play.google.com/store/apps/details?id=com.callstack.reactnativepaperexample&pcampaignid=web_share](https://play.google.com/store/apps/details?id=com.callstack.reactnativepaperexample&pcampaignid=web_share)

pueden instalar la libreria en sus celulares para que vayan probando los componentes

## Contenido

### Componentes Específicos de React Native:
```
Componentes básicos de React Native: View, Text, Image, ScrollView, FlatList.
Diferencias entre los componentes de React (DOM) y React Native (nativos).
```

View : 
un div sin scroll, un container compatible con layout con flexbox, styles, algun evento touch y controles de accesibilidad

Text : 
Muestra estilos y hace nest de strings de texto incluso maneja eventos touch

Image : 
Muestra distintos tipos de imagenes

ScrollView : 
Un contenedor scrolleable que puede contener multibples componentes y views

FlatList :
A performant interface for rendering basic, flat lists, supporting the most handy features:
- Fully cross-platform
- Optional horizontal mode
- Header support
- Footer support
- Separator support
- Pull to Refresh
- Scroll loading
- ScrollToIndex support
- Multiple column support

SectionList : 
A performant interface for rendering sectioned lists, supporting the most handy features:
- Fully cross-platform.
- Configurable viewability callbacks
- List header support
- List footer support
- Item separator support
- Section header support
- Section separator support
- Heterogeneous data and item rendering support
- Pull to Refresh
- Scroll loading

```jsx
<FlatList
        data={DATA}
        renderItem={({item}) => <Item title={item.title} />}
        keyExtractor={item => item.id}
      />
```


#### React DOM and React Native have in common:
1. They both use the same core React library.
2. They both use the same component-based architecture, which means that developers can break down their applications into smaller, more manageable pieces.
3. They both use JavaScript as their programming language, and JSX as their templating language.
4. Both React DOM and React Native use virtual DOMs to render their applications.
5. Both React DOM and React Native also use the same styling techniques and components, through React Native's is a bit different.
6. They both utilize Chrome DevTools for debugging applications.
7. They use the same JavaScript APIs.
8. Both were developed in Meta. React was developed by a software engineer named Jordan Walke while React Native was born from a hackathon.

#### Differences
React DOM uses HTML, CSS, and JavaScript for layout and styling, and allows developers to create interactive user interfaces. React Native, on the other hand, uses native UI components and APIs to create cross-platform mobile applications.


### Estilos
```
Uso de StyleSheet en lugar de CSS.
Flexbox para el diseño de interfaces (similar a web, pero con pequeñas diferencias).
```

#### Flexbox

```jsx
<View
      style={[
        styles.container,
        {
          // Try setting `flexDirection` to `"row"`.
          flexDirection: 'column',
        },
      ]}>
      // 1/6 del contenedor
      <View style={{flex: 1, backgroundColor: 'red'}} />
      // 2/6 del contenedor
      <View style={{flex: 2, backgroundColor: 'darkorange'}} />
      // 3/6 - 1/2 del contenedor
      <View style={{flex: 3, backgroundColor: 'green'}} />
    </View>
```

**Flex directions**
```js
values = { ['column', 'row', 'row-reverse', 'column-reverse'] }
```

**Layout direction ( { direction: value } )**
```jsx
values = { ["ltr", "rtl"] }
```

justifyContent, alignItems, alignSelf, alignContent equal as React web
alignContent only has effect when items are wrapped to multiple lines usin flexWrap

**Flex Wrap**
```jsx
// flexWrap
 values = { ['wrap', 'nowrap'] }
```


**Flex Basis, Grow, and Shrink**
- **flexBasisis :** is an axis-independent way of **providing the default size of an item along the main axis**.  The size of the item before any `flexGrow` and `flexShrink` calculations are performed.
- **flexGrow :**  describes how much space within a container should be distributed among its children along the main axis
- `flexGrow` accepts any floating point value >= 0, with 0 being the default value. A container will distribute any remaining space among its children weighted by the children’s `flexGrow` values.
- **flexShrink :** describes how to shrink children along the main axis in the case in which the total size of the children overflows the size of the container on the main axis. `flexShrink` accepts any floating point value >= 0, with 0 being the default value ==**(on the web, the default is 1)**==. A container will shrink its children weighted by the children’s `flexShrink` values.

**Row Gap, Column Gap and Gap**
- `rowGap`sets the size of the gap (gutter) between an element's rows
- `columnGap`sets the size of the gap (gutter) between an element's columns
- `gap` sets the size of the gap (gutter) between rows and columns. It is a shorthand for `rowGap` and `columnGap`

**Width and Height**
The `width` property specifies the width of an element's content area. Similarly, the `height` property specifies the height of an element's content area.
- `auto` (**default value**) React Native calculates the width/height for the element based on its content
- `pixels` Defines the width/height in absolute pixels. Depending on other styles set on the component, this may or may not be the final dimension of the node.
- `percentage` Defines the width or height in percentage of its parent's width or height, respectively.

**Absolute and relative**
`postition: absolute` and `postition: relative` behaves equal as react web

### Navegación:

```
Configuración y uso de React Navigation.
Diferentes tipos de navegadores: Stack Navigator, Tab Navigator, Drawer Navigator.
```

https://reactnative.dev/docs/navigation#react-navigation

Envolver la aplicacion en el Navigation provider
```jsx
import * as React from 'react';  
import {NavigationContainer} from '@react-navigation/native';  
  
const App = () => {  
return (  
<NavigationContainer>  
{/* Rest of your app code */}  
</NavigationContainer>  
);  
};  
  
export default App;
```

Instanciar el Stack y envolver las Screen en un Navigator : 
- `name = 'Home'` va a ser el nombre por el cual acceder a la vista
- cada componente recibe por props una instancia de `navigation`, se puede usar `navigation.navigate` en un `onPress` para navegar mediante un botón a distintas pantallas.
- tambien recibe `route` donde podemos acceder al nombre mediante `route.params.name`
```jsx
import * as React from 'react';  
import {NavigationContainer} from '@react-navigation/native';  
import {createNativeStackNavigator} from '@react-navigation/native-stack';  
  
const Stack = createNativeStackNavigator();  
  
const MyStack = () => {  
return (  
<NavigationContainer>  
<Stack.Navigator>  
<Stack.Screen  
name="Home"  
component={HomeScreen}  
options={{title: 'Welcome'}}  
/>  
<Stack.Screen name="Profile" component={ProfileScreen} />  
</Stack.Navigator>  
</NavigationContainer>  
);  
};
```
Button : 
```jsx
<Button  
title="Go to Jane's profile"  
onPress={() =>  
navigation.navigate('Profile', {name: 'Jane'})  
}  
/>
```


### Apis Nativas

Acceso a APIs Nativas:

`Uso de librerías (EXPO) para acceder a funcionalidades nativas (ej. cámara, ubicación, almacenamiento) Introducción a react-native-gesture-handler y react-native-reanimated`
camera : https://docs.expo.dev/versions/latest/sdk/camera/
ubicacion : https://docs.expo.dev/versions/latest/sdk/location/
almacenamiento : https://docs.expo.dev/develop/user-interface/store-data/
gesture handler : https://docs.expo.dev/versions/latest/sdk/gesture-handler/
reanimated : https://docs.expo.dev/versions/latest/sdk/reanimated/

#### Camera :
``` tsx
import { CameraView, useCameraPermissions } from 'expo-camera';
import { useState } from 'react';
import { Button, StyleSheet, Text, TouchableOpacity, View } from 'react-native';

export default function App() {
// facing se usa en el componete CameraView como prop ['back','front']
  const [facing, setFacing] = useState('back');
  const [permission, requestPermission] = useCameraPermissions();

  if (!permission) {
    // Camera permissions are still loading.
    return <View />;
  }

  if (!permission.granted) {
    // Camera permissions are not granted yet.
    return (
      <View style={styles.container}>
        <Text style={{ textAlign: 'center' }}>We need your permission to show the camera</Text>
        <Button onPress={requestPermission} title="grant permission" />
      </View>
    );
  }

  function toggleCameraFacing() {
    setFacing(current => (current === 'back' ? 'front' : 'back'));
  }

  return (
    <View style={styles.container}>
      <CameraView style={styles.camera} facing={facing}>
        <View style={styles.buttonContainer}>
          <TouchableOpacity style={styles.button} onPress={toggleCameraFacing}>
            <Text style={styles.text}>Flip Camera</Text>
          </TouchableOpacity>
        </View>
      </CameraView>
    </View>
  );
}
```

#### Location :
```tsx 
import React, { useState, useEffect } from 'react';
import { Platform, Text, View, StyleSheet } from 'react-native';

import * as Location from 'expo-location';

export default function App() {
  const [location, setLocation] = useState(null);
  const [errorMsg, setErrorMsg] = useState(null);

  useEffect(() => {
    (async () => {
      
      let { status } = await Location.requestForegroundPermissionsAsync();
      if (status !== 'granted') {
        setErrorMsg('Permission to access location was denied');
        return;
      }

      let location = await Location.getCurrentPositionAsync({});
      setLocation(location);
    })();
  }, []);

  let text = 'Waiting..';
  if (errorMsg) {
    text = errorMsg;
  } else if (location) {
    text = JSON.stringify(location);
  }

  return (
    <View style={styles.container}>
      <Text style={styles.paragraph}>{text}</Text>
    </View>
  );
}
```

#### Storage : 


### React Native Paper
https://reactnativepaper.com/

#### Components

Animated Floating Action Button: 
![[Pasted image 20240616124315.png]]

Activity Indicator : 
![[Pasted image 20240616124407.png]]

Appbar : 
![[Pasted image 20240616124429.png]]

Avatar : 
![[Pasted image 20240616124452.png]]

Badges : 
![[Pasted image 20240616124514.png]]

Bottom Navigation Bar : 
![[Pasted image 20240616124542.png]]

Bottom Navigation : 
![[Pasted image 20240616124609.png]]

Button : 
![[Pasted image 20240616124650.png]]

Card : 
![[Pasted image 20240616124717.png]]

Checkbox : 
![[Pasted image 20240616124738.png]]

Checkbox Item : 
![[Pasted image 20240616124832.png]]

Chip : 
![[Pasted image 20240616124858.png]]

Data Table : 
![[Pasted image 20240616124956.png]]

Dialog : 
![[Pasted image 20240616125042.png]]

Divider : 
![[Pasted image 20240616125102.png]]

Floating Action Button : 
![[Pasted image 20240616125144.png]]

Icon Button : 
![[Pasted image 20240616125229.png]]

Icon  : 
![[Pasted image 20240616125348.png]]

List.Accordion : 
![[Pasted image 20240616125459.png]]

List.Accordion.Group : 
![[Pasted image 20240616125555.png]]

List Section :
![[Pasted image 20240616125622.png]]

List.Item : 
![[Pasted image 20240616125649.png]]

Menu : 
![[Pasted image 20240616125720.png]]

Progress Bar : 
![[Pasted image 20240616125752.png]]

Radio Button : 
![[Pasted image 20240616125809.png]]

Radio Button Group : 
![[Pasted image 20240616125857.png]]

Radio Button Item : 
![[Pasted image 20240616125925.png]]

Search Bar : 
![[Pasted image 20240616125945.png]]

Segmented Buttons : 
![[Pasted image 20240616130131.png]]
Snackbar : 
![[Pasted image 20240616130148.png]]
Surface : 
![[Pasted image 20240616130402.png]]

Switch : 
![[Pasted image 20240616130419.png]]

Typography : 
![[Pasted image 20240616130431.png]]

TextInput : 
![[Pasted image 20240616130459.png]]

Toggle Button : 
![[Pasted image 20240616130528.png]]

Tooltip : 
![[Pasted image 20240616130557.png]]

TouchableRipple : 
![[Pasted image 20240616130631.png]]

Theme : 


Theming with React Navigation : 

```tsx
import { FontAwesome6 } from '@expo/vector-icons';
import { useState } from 'react';
import { Text, View } from 'react-native';
import { ToggleButton } from 'react-native-paper';
  
const icons = [
   <FontAwesome6
      name="location-arrow"
      size={18}
      color="black"
      style={{ transform: [{ rotate: '275deg' }] }}
   />,
   <FontAwesome6
      name="location-arrow"
      size={18}
      color="red"
      style={{ transform: [{ rotate: '275deg' }] }}
   />,
   <FontAwesome6
      name="location-arrow"
      size={18}
      color="blue"
      style={{ transform: [{ rotate: '275deg' }] }}
   />,
];
  
export default function TabFiveScreen() {
   const [toggleIconIndex, setToggleIconIndex] = useState(0);
  
   const toggleIconHandler = () => {
      setToggleIconIndex(prev => (prev === icons.length - 1 ? 0 : prev + 1));
   }
  
   console.log(toggleIconIndex)
  
   return (
      <View>
         <Text style={{ color: '#f00' }}> Cuenta</Text>
         <ToggleButton
            onPress={() => toggleIconHandler()}
            icon={() => icons[toggleIconIndex]}
         />
      </View>
   );
}
```
### Notes :
##### StyleSheet.Flatten : 
```tsx
import { View, Text, StyleSheet, useColorScheme } from "react-native";
import React from "react";
import { Button } from "react-native-paper";
import { Colors } from "@/constants/Colors";

const SignUp = () => {
  const theme = Colors[useColorScheme() ?? "light"];

  // Definir los estilos estáticos
  const staticStyles = StyleSheet.create({
    buttonsContainer: {
      display: "flex",
      flexDirection: "column",
      alignItems: "center",
      gap: 5,
    },
    signUpButtonText: {
      fontSize: 15,
      paddingVertical: 7,
    },
    hasAccountText: {
      fontSize: 15,
      // fontWeight: 200
    },
  });

  // Combinar estilos dinámicos con estáticos
  const dynamicStyles = {
    hasAccountButton: {
      width: 180,
      borderRadius: 100,
      backgroundColor: theme.tint,
    },
    signUpButton: {
      borderRadius: 100,
      width: "80%",
      backgroundColor: theme.primaryButtonBg,
    },
  };

  const styles = StyleSheet.flatten([staticStyles, dynamicStyles]);

  return (
    <View>
      <Text>sign-up</Text>
      <View style={styles.buttonsContainer}>
        <Button
          labelStyle={styles.signUpButtonText}
          style={styles.signUpButton}
          mode="contained"
          onPress={() => console.log("Pressed")}
          uppercase
        >
          Registrarse
        </Button>
        <Button
          labelStyle={styles.hasAccountText}
          style={styles.hasAccountButton}
          mode="contained"
          onPress={() => console.log("Pressed")}
        >
          Ya tengo cuenta
        </Button>
      </View>
    </View>
  );
};

export default SignUp;

```

