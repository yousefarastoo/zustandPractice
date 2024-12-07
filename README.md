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

# Immer middleware

* The Immer middleware enables you to use immutable state in a more convenient way.
* Also, with Immer, you can simplify handling immutable data structures in Zustand.


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
first define type state and action for counter
in app/fax/lisa/store/type/CounterType : 

```sh
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
    import {immer} from "zustand/middleware/immer"

    export const CreateCounter:StateCreator<CounterSlice,[["zustand/immer",never]],[],CounterSlice> =(set)=>({
        inc() {
            // set(state=>({...state,counter:state.counter+1}))
            // for updating and changing state with help of immer now wa can :
            set(state=>{state.counter = state.counter+1})
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
import {immer} from "zustand/middleware/immer"
import {Store} from "./type/storeType"
import { CreateCounter } from "./slicer/createCounter"

export const useStore = create<Store>()(immer(
(...a)=>({
    ...CreateCounter(...a),
})
))

```
