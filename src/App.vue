<template>
    <div style="width: 100%; height: 95%; padding-top: 16px; margin: 0 auto;">
        <DiagramEditor  :editable    = "true"
                        :elements    = "elements"
                        @add-item    = "addNewItem" 
                        @delete-item = "deleteItem" 
                        
                        @add-connection="addNewConnection"
                        />
    </div>
</template>

<script setup lang="ts">
import { reactive } from 'vue';
import AddConnectionCommand from './components/diagram-editor/commands/AddConnectionCommand';
import AddItemCommand from './components/diagram-editor/commands/AddItemCommand';
import DeleteCommand from './components/diagram-editor/commands/DeleteCommand';
import HistoryManager from './components/diagram-editor/commands/HistoryManager';
import DiagramEditor from './components/diagram-editor/DiagramEditor.vue';
import { createConnection, createItem } from './components/diagram-editor/helpers';

import { ConnectionPoint, DiagramElement, Item, ItemConnection } from './components/diagram-editor/types';


let elements: DiagramElement[] = reactive([
    //...createTestConnections(),

    createItem({ id: 'a1', title: 'a1', w: 100, h: 80 }),
    createItem({ id: 'a2', title: 'a2', w: 90,  h: 90 }),
    createItem({ id: 'a3', title: 'a3', w: 200, h: 70 }),
    
    //createConnection('a1', 'a2'),
    //createConnection('a1', 'a3', { type: ConnectionType.CURVE, style: ConnectionStyle.DOTTED }),
    //createConnection('a2', 'a3', { type: ConnectionType.CURVE, style: ConnectionStyle.DASHED, color: "red", thick: 5 }),

    // createItem( { title: 'This is a text and can be quite long!', component: "Text", supportsRoundable: false } ),

    // createItem( { title: 'Line 1',     w: 400, h: 30, component: "Line", supportsRoundable: false } ),
    // createItem( { title: 'Line 2',     w: 400, h: 30, component: "Line", backgroundColor: 'red', componentOptions: { thick: 5 },  supportsRoundable: false } ),
    
    // createItem( { id: 't1', title: 'Triangle 1', w: 200, h: 150, component: "Triangle", supportsRoundable: false } ),
    // createItem( { id: 't2', title: 'Triangle 2', w: 200, h: 150, component: "Triangle", supportsRoundable: false } ),
    // createConnection('t1', 't2', { type: ConnectionType.CURVE, style: ConnectionStyle.DASHED, color: "green", thick: 3 }),
   
    // createItem( { id: 's1', title: 'Star 1', w: 100, h: 100, component: "Star", supportsRoundable: false } ),
    // createItem( { id: 's2', title: 'Star 2', w: 60,  h: 60,  component: "Star", supportsRoundable: false } ),
    // createItem( { id: 's3', title: 'Star 3', w: 130, h: 130, component: "Star", supportsRoundable: false } ),
    // createConnection('s1', 's2'),
    // createConnection('s2', 's3'),
    // createConnection('s3', 's1'),

    //createItem( { title: 'Item (no resize)',  component: "Rectangle", supportsResizable: false } ),
    
    //createItem( { title: 'Item D',            component: "CustomShape", w: 300, h: 300, supportsRoundable: false } ),
    //createItem( { title: 'Ellipse 1',         component: "Ellipse",     w: 400, h: 200, supportsRoundable: false } ),
    
    //createItem( { title: 'My Image',          component: "Image",       w: 250, h: 250, componentOptions: { src : "https://images.unsplash.com/photo-1496171367470-9ed9a91ea931?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80" }} ),
    //createItem( { title: 'My Image',          component: "Image",       w: 800, h: 400, componentOptions: { src : "https://stmicroelectronics-my.sharepoint.com/:i:/r/personal/giuseppe-angelo_randazzo_st_com/Documents/_public/8d-action-list.png?csf=1&web=1&e=vqfufX" }} ),

]);


function createTestConnections(): DiagramElement[] {
    return [
        createItem({ id: 's1', title: 's1', w: 100, h: 80 }),

        createItem({ id: 't1', title: 't1', w: 90,  h: 90 }),
        createItem({ id: 't2', title: 't2', w: 90,  h: 90 }),
        createItem({ id: 't3', title: 't3', w: 90,  h: 90 }),
        createItem({ id: 't4', title: 't4', w: 90,  h: 90 }),
        createItem({ id: 't5', title: 't5', w: 90,  h: 90 }),

        createConnection('s1', 't1', { fromPoint: ConnectionPoint.RIGHT, toPoint: ConnectionPoint.LEFT   }),
        createConnection('s1', 't2', { fromPoint: ConnectionPoint.RIGHT, toPoint: ConnectionPoint.RIGHT  }),
        createConnection('s1', 't4', { fromPoint: ConnectionPoint.RIGHT, toPoint: ConnectionPoint.TOP    }),
        createConnection('s1', 't3', { fromPoint: ConnectionPoint.RIGHT, toPoint: ConnectionPoint.BOTTOM }),
        createConnection('s1', 't5', { fromPoint: ConnectionPoint.RIGHT, toPoint: ConnectionPoint.CENTER }),

    ];
}

function addNewItem(item: Item, historyManager: HistoryManager) {
    historyManager.execute(new AddItemCommand(elements, item));    
}

function deleteItem(item: Item, historyManager: HistoryManager) {
    historyManager.execute(new DeleteCommand(elements, item));    
}

function addNewConnection(c: ItemConnection, historyManager: HistoryManager) {
    //elements.push(c)
    historyManager.execute(new AddConnectionCommand(elements, c));    
}


</script>