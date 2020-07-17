# Minkowski trajectory simulator
## Aim
To create this:
https://www.youtube.com/watch?v=8o2okVL9NjQ
with the ability to:
- enter in multiple trajectories (as a quadratic beizer or continuous function)
    - relative to different objects e.g. around an already moving object
- play said tragectories
- from different points of view


## Method
- direct render everything on canvas
    - precalc all points, derivatives, POVs at each frame
- use SVG
    - also precalc, but using an SVG renderer

## TODO
- multiple line renderer
- tragectory calculator
    0. evaluate each function as if it were in 0 reference frame
    1. build a hierarchy of things to calculate
    2. use position addition to add position in each case.

    - 
```javascript
let trajectoryDefs = [{}];
let trajectories=[{}];
function getTrajectory(type, params)//=> returns [y,t] pairs
function getAllTrajectories(trajectoryDefs: [{
    dep: x,
    type:"biezer"||"function",
    param: [[1,1],[2,2],[4,3]] || (t)=>Math.sin(t)
}]) // returns [y_0,t_0,t_rel] (y_rel is always 0)
function renderTrajectories(trajectories,relativeTo,t_rel){
    // identify the v_0 at t_rel in relativeTo
    for (let t of trajectories){
        // transform everyone into v_0 by taking delta y_0, delta t_0 and transforming by v_0 to get t_rel_rel and y_rel_rel
        // plot all y_rel_rel and t_rel_rel
        plotSeries(y_rel_rel, t_rel_rel);
    }
}
function updateTrajectories(){
    trajectories=getAllTrajectories(trajectoryDefs);
    t_rel=0;
}

setInterval(()=>{
    renderTrajectories(trajectories,relativeTo,t_rel);
    if (t_rel<t_max)t_rel+=0.01;
},100);
```