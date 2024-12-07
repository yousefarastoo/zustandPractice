# zustandPractice
```bash
├── component
│   └── component.tsx
├── page.tsx
├── store
│   ├── slicer
│   │   ├── createCounter.tsx
│   │   └── createUser.tsx
│   ├── store.tsx
│   └── type
│       ├── counterType.ts
│       ├── storeType.ts
│       └── userType.ts
└── store.ts
```

first define type state and action for counter  :
in app/fax/lisa/store/type/CounterType : 

```sh

import { create } from "zustand";
import { type StateCreator } from "zustand";

type CounterState = {
    counter:number
}

type CounterAction = {
    inc:()=>void,
    reset:()=>void,
    dec:()=>void,
    incNumberPluse:(number:number)=>void
}


export type CounterSlice = CounterAction & CounterState;

```

in app/fax/lisa/store/type/counterType

```sh
import { create } from "zustand";
import { type StateCreator } from "zustand";
type CounterState = {
    counter:number
}
type CounterAction = {
    inc:()=>void,
    reset:()=>void,
    dec:()=>void,
    incNumberPluse:(number:number)=>void
}

export type CounterSlice = CounterAction & CounterState;

```



in app/fax/lisa/store/slicer/createCounter.tsx

```sh
    import { type StateCreator } from "zustand"
    import { type CounterSlice } from "../type/counterType"


    export const CreateCounter:StateCreator<CounterSlice,[],[],CounterSlice> =(set)=>({
        inc() {
            set(state=>({...state,counter:state.counter+1}))
        },
        dec() {
            set(state=>({...state,counter:state.counter-1}))
        },
        reset() {
            set(state=>({...state,counter:0}))
        },
        incNumberPluse(number) {
            set(state=>({...state,counter:state.counter+number}))

        },
        counter:0,
    }) 

```

in app/fax/lisa/store/type/storeType

```sh

import {type CounterSlice} from "../type/counterType"
export type Store = CounterSlice
```

in app/fax/lisa/store/store.tsx

```sh
import {create} from "zustand"
import {Store} from "./type/storeType"
import { CreateCounter } from "./slicer/createCounter"

export const useStore = create<Store>()((...a)=>({
    ...CreateCounter(...a),
}))

```
===============================================================


# Immer middleware

* The Immer middleware enables you to use immutable state in a more convenient way.
* Also, with Immer, you can simplify handling immutable data structures in Zustand.


```sh
npm install immer
 ```

```bash
├── component
│   └── component.tsx
├── page.tsx
├── store
│   ├── slicer
│   │   ├── createCounter.tsx
│   │   └── createUser.tsx
│   ├── store.tsx
│   └── type
│       ├── counterType.ts
│       ├── storeType.ts
│       └── userType.ts
└── store.ts
```
first define type state and action for counter  :
in app/fax/lisa/store/type/CounterType : 

```sh

import { create } from "zustand";
import { type StateCreator } from "zustand";

type CounterState = {
    counter:number
}

type CounterAction = {
    inc:()=>void,
    reset:()=>void,
    dec:()=>void,
    incNumberPluse:(number:number)=>void
}


export type CounterSlice = CounterAction & CounterState;

```

in app/fax/lisa/store/type/counterType

```sh
import { create } from "zustand";
import { type StateCreator } from "zustand";
type CounterState = {
    counter:number
}
type CounterAction = {
    inc:()=>void,
    reset:()=>void,
    dec:()=>void,
    incNumberPluse:(number:number)=>void
}

export type CounterSlice = CounterAction & CounterState;

```

in app/fax/lisa/store/slicer/createCounter.tsx

```sh
    import { type StateCreator } from "zustand"
    import { type CounterSlice } from "../type/counterType"


    export const CreateCounter:StateCreator<CounterSlice,[],[],CounterSlice> =(set)=>({
        inc() {
            set(state=>({...state,counter:state.counter+1}))
        },
        dec() {
            set(state=>({...state,counter:state.counter-1}))
        },
        reset() {
            set(state=>({...state,counter:0}))
        },
        incNumberPluse(number) {
            set(state=>({...state,counter:state.counter+number}))

        },
        counter:0,
    }) 

```


in app/fax/lisa/store/type/storeType

```sh

import {type CounterSlice} from "../type/counterType"
export type Store = CounterSlice & UserSlicer
```

in app/fax/lisa/store/store.tsx

```sh
import {create} from "zustand"
import {Store} from "./type/storeType"
import { CreateCounter } from "./slicer/createCounter"

export const useStore = create<Store>()((...a)=>({
    ...CreateCounter(...a),
}))

```

app/fax/lisa/store/type/store
```sh
import {create} from "zustand"
import {Store} from "./type/storeType"
import { CreateCounter } from "./slicer/createCounter"
import {userCreator} from "./slicer/createUser"



export const useStore = create<Store>()((...a)=>({
    ...CreateCounter(...a),
}))
```

