# Prompt: Cinematic Interactive 3D Aquarium in a Lived-In Keeper's Corner

## Objective

Create a polished, visually rich, interactive **3D aquarium and the inhabited room corner around it**, delivered as a **single self-contained HTML file**.

The aquarium contains three recognizable clownfish, a giant anemone, dense plants, coral, rocks, layered substrate, ruins, driftwood, a treasure chest, bubbles, small creatures, and hidden discoveries. Outside the glass, build the keeper's everyday world: a worn cabinet, a working desk lamp, window blinds, houseplant, mug with rising steam, food jar, notebook, care equipment, scattered objects, and an animated tabby cat named **Milo**.

Both worlds must belong to the **same orbitable Three.js scene**. Objects outside the tank have real depth, lighting, contact shadows, and useful interactions. Milo watches the fish; his gentle glass tap briefly startles nearby fish. Clicking the food jar feeds the aquarium. Clicking the cabinet door reveals supplies. Clicking the notebook moves an actual page.

Create a cozy, cinematic, slightly magical miniature that feels maintained, used, and loved. Include believable wear and small imperfections while keeping the fish, major props, and user controls easy to see.

Use **Three.js imported from a CDN** for all 3D rendering. Generate geometry, materials, shaders, textures, labels, diagrams, particles, and animation procedurally inside the HTML. Use no external images, models, audio, fonts, or other art assets.


---

# Core Technical Requirements

* Produce exactly one complete, working `.html` file.
* Put all CSS, JavaScript, GLSL, and generated assets inside that file. Use `<script type="module">`.
* Import Three.js, OrbitControls, and any Three.js addons from compatible, explicitly pinned CDN ES-module URLs.
* Use an import map so addons that import the bare module name `three` resolve correctly.
* No external image textures, 3D models, HDR environment maps, audio files, fonts, or external shader files.
* Runtime-generated `CanvasTexture`, `DataTexture`, procedural environment maps, and text drawn on an in-memory canvas are allowed. Draw every label and diagram locally from code.
* Do not replace the room or aquarium with a static image, CSS illustration, or pre-rendered backdrop.
* No build tools, package installation, backend, UI framework, physics library, or heavy post-processing dependency.
* Launch without JavaScript errors, shader compilation errors, missing uniforms, invalid geometry, or broken imports.
* Support opening the HTML in a modern browser with module support, or serving it with a simple local HTTP server. CDN imports require an internet connection.
* Fill the viewport, respond to resizing, and remain usable with mouse and touch input.
* Target smooth animation near 60 FPS on a modern desktop using low-to-medium-poly geometry, shared resources, batching, instancing, and bounded pools.

Use one coherent dependency setup, for example:

```html
<script type="importmap">
{
  "imports": {
    "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
    "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
  }
}
</script>
<script type="module">
import * as THREE from "three";
import { OrbitControls } from "three/addons/controls/OrbitControls.js";
import { mergeGeometries } from "three/addons/utils/BufferGeometryUtils.js";
</script>
```

The geometry utility import is optional if your implementation does not need it. If using another version, update the entire import map consistently.

---

# Art Direction

Create a cozy, cinematic keeper's corner in a dark room. The aquarium is the main living focal point, with a believable everyday world around it.

Combine:

* Clear tinted glass, gently moving water, warm aquarium light, and soft blue caustics.
* Recognizable stylized clownfish and a lush miniature reef.
* Walnut, worn teal paint, muted brass, terracotta, cream paper, and soft textiles outside the tank.
* A warm desk lamp balanced with cooler window and aquarium light.
* Independent, gentle movement: swimming fish, swaying anemone, breathing cat, blinking eyes, curling tail, rising steam, ticking clock, and slow room-plant movement.
* Small humorous discoveries, handwritten-looking notes, and traces of ordinary maintenance.

The corner should look used and cared for. Include a chipped mug, cup ring, loose food flakes, a crooked print, tangled cords, worn cabinet edges, localized algae, and a notebook left open. These details should have plausible causes and locations.

Keep negative space for swimming and readable silhouettes. Cluster objects deliberately rather than spacing every prop evenly. Avoid a sterile product showroom, uniformly pristine surfaces, random clutter, opaque dirty water, and a neon color palette.

Give the whole composition a calm, premium atmosphere with details worth discovering when the camera is rotated or zoomed.

---

# Scene Layout

## Aquarium Dimensions and Coordinates

Use a rectangular open-top tank approximately `7` units wide, `4.5` units tall, and `3.5` units deep, centered near the world origin.

One useful coordinate convention is:

* Tank sides: approximately `x = -3.5 … 3.5`.
* Tank bottom and rim: approximately `y = -2.2 … 2.25`.
* Tank depth: approximately `z = -1.75 … 1.75`, with positive Z toward the front.
* Waterline: approximately `y = 2.03`.
* Cabinet countertop: approximately `y = -2.55`, touching the bottom of the tank's plinth.
* Room floor: approximately `y = -5.3`.
* Back wall: approximately `z = -2.9`.

These are composition guides, not permission to leave gaps or intersections. Align supporting surfaces after choosing the actual dimensions.

## Complete Keeper's Corner

Build a compact floor-and-wall diorama roughly `12–14` units wide. The countertop extends beyond the tank to provide visible areas for household objects. The cabinet, floor, wall, stool, and room props must exist as actual 3D geometry.

Suggested arrangement:

* Aquarium: above the cabinet, central and visually dominant.
* Window with blinds and a houseplant: behind the left side.
* Brass-and-green desk lamp and mug: on the left countertop extension.
* Food jar: on a visible front ledge, fully outside the glass and easy to click.
* Open notebook, pencil, cloth, and scattered flakes: across the front countertop edge.
* Filter canister and net: toward the right or rear side, with believable hose routing.
* Milo: seated on a clear area of the right countertop, visible beside the tank and close enough to reach its outer glass.
* Stool: tucked partly beneath the countertop, physically separate from Milo's body.
* Clock and slightly crooked fish diagram: on the back wall.
* Books and supplies: on the open shelf and inside the hinged cabinet.
* Yarn ball and trailing thread: on the floor near the stool.

Maintain contact between props and their supporting surfaces. Milo must not intersect the tabletop or glass. Keep doors, tails, leaves, and cords clear enough to animate without obvious clipping.


---

# Background and Room Atmosphere

Use a dark procedural gradient, inverted sphere, or studio backdrop behind the **modeled keeper's corner**. Suggested colors are `#08111f`, `#102b42`, and `#02070d`. Add a subtle vignette and soft halo.

The actual room must include a visible floor slab and a back wall. Give the floor faint shadows, plank seams, varied wear, and soft reflected light. Give the wall subtle stains, painted trim or lower paneling, and the window, clock, and framed print described below.

Make the room comfortable to orbit. Use one-sided wall surfaces, a cutaway arrangement, or controlled wall visibility when the camera moves behind it. The back wall must not become a solid obstruction that hides the entire aquarium during normal camera use.

Keep the main composition readable at night. Dim the room gradually while retaining the warm desk-lamp pool, cool window light, fish silhouettes, anemone glow, and Milo's outline.

---

# Required Exterior Decorations

All exterior groups in this section are mandatory. Their presence must be visible in geometry; a text label or toast alone is not an implementation. Simplify mesh detail when necessary while keeping each group recognizable.

## 1. Worn Walnut Countertop and Painted Cabinet

* Build a solid walnut countertop wider and slightly deeper than the aquarium plinth. Show thickness, subtle procedural grain, small edge chips, and a few directional scratches.
* Use muted teal painted cabinet panels, trim, feet, seams, and brass or dark-metal handles.
* Include an open side shelf with unevenly stacked books and a closed storage compartment.
* Build one cabinet door as a separate group with its pivot at a real hinge. Clicking it smoothly opens the door by roughly 60–70 degrees; clicking again closes it.
* Behind the door, place folded towels, a small bucket with a handle, spare filter media or refill jars, and basic aquarium supplies. These objects must exist before the door opens and remain in place.
* Keep the handle and sticky note attached to the moving door. Do not move the entire cabinet when opening it.

## 2. Books, Labels, and the Reminder Note

* Create several physical books with covers, page blocks, visible spines, and small variations in size, rotation, and alignment.
* Suitable fictional titles include `REEF ATLAS`, `SMALL WORLDS`, and `THE SLOW LIFE`.
* Attach a slightly crooked paper note to a cabinet door: `Milo is NOT in charge of feeding.`
* Generate the typography and subtle paper grain locally, using canvas textures or geometry. No downloaded book covers or fonts.
* Make these details readable when zoomed in without turning them into oversized interface labels.

## 3. Adjustable Desk Lamp and Power Cord

* Create a separate desk lamp on the countertop: weighted base, articulated brass arm, visible joints, green or teal shade, an open underside, rim, and a glowing bulb.
* Add an actual warm light near the bulb so nearby wood, mug, and notebook receive a believable pool of illumination.
* Route a slightly tangled cord from the base over or behind the countertop, down toward the floor, and to a small plug or wall socket.
* Clicking the physical lamp switches the same Day/Night state used by the HTML control. Update the button state and all relevant lighting together.
* Preserve readable room detail in night mode; do not make every exterior object disappear into black.

## 4. Window, Uneven Blinds, and Wall Clock

* Build a small framed window with a sill and several individual blind slats, slightly varied in tilt or spacing.
* Include thin hanging blind cords. Model the frame and slats with real depth.
* Generate the view outside procedurally: a muted daytime gradient transitioning to a darker blue night gradient with a small moon.
* Add an analog wall clock with a face, hour marks, frame, and separate hour, minute, and second hands.
* Advance the hands from the central animation clock. A subtle once-per-second tick of the second hand is sufficient. The hands freeze with the simulation when Pause is active.

## 5. Houseplant in a Chipped Terracotta Pot

* Add a hollow-looking pot with a rim, visible soil, slight asymmetry, and a small chip or worn patch.
* Use curved stems and several heart-shaped or broad leaves with visible central veins, varied sizes, bends, and orientations.
* Include a trailing vine hanging over the pot or countertop edge.
* Animate leaves with separate phases. Indoor movement is much weaker than underwater swaying.
* Keep the plant outside the aquarium. Check that leaves and stems do not accidentally grow through the glass.

## 6. Chipped Mug, Tea, Steam, and Cup Ring

* Make a real hollow mug with a handle, an inner wall, a slightly uneven rim, and a small visible chip.
* Add a dark tea or coffee surface inside the mug.
* Create a small bounded steam system above the drink. Wisps rise, drift, fade, and recycle; they remain anchored to the mug's world position.
* Place an incomplete cup ring and a few subtle drips on the countertop nearby.
* Keep the effect delicate. Steam is air vapor outside the tank and must not behave like underwater bubbles.

## 7. Interactive Food Jar and Spilled Flakes

* Place a recognizable jar on the **front countertop ledge**, outside the tank and visible from the default angle.
* Give it a body, paper label, separate lid, rim or grip ridges, and a few loose flakes nearby.
* Suggested label: `REEF / DAILY FLAKES / A tiny pinch.`
* Clicking the jar rocks or shakes the jar and its loose lid briefly, then drops 8–15 food particles into a safe location inside the aquarium.
* Use the same food pool, cooldown, fish attraction, nibbling, and expiration logic as the Feed fish button and water-surface interaction.
* Do not substitute a feeding message for actual food particles or fish behavior.

## 8. Open Field Notebook, Moving Page, Pencil, and Bookmark

* Build a small open notebook with a cover, two visible pages or page stacks, a spine, and slight page curl or unevenness.
* Draw handwritten-looking observations, ruled lines, and a simple clownfish sketch procedurally.
* Possible notes: `DAY 042`, `03 fish / 01 cat`, `Algae: tomorrow.`, and `Milo: suspicious.`
* Add a pencil with a graphite tip and a narrow bookmark protruding from the book.
* Clicking the notebook visibly lifts or turns one page around the spine, then lets it settle. Use a real mesh or group animation and a bounded state transition.
* A short caption may accompany the action, but the page itself must move.

## 9. Folded Cloth, Splashes, and Escaped Gravel

* Add a soft-looking cleaning cloth with several folds, an irregular edge, and a slightly rumpled placement on the front ledge.
* Use a subdivided surface or simple overlapping folded geometry rather than a perfectly flat rectangle.
* Add restrained dried splashes and small damp marks near the cloth and tank rim.
* Scatter a few individual gravel pieces on the floor near the cabinet, as though some substrate escaped during maintenance.
* Leave clear areas of tabletop. The mess should read as a few recent actions, not uniform procedural noise across every surface.

## 10. Filter Canister, Routed Hoses, and Thermometer

* Add a small exterior canister or aquarium pump with a cap, base, label, and visible hose connections.
* Route one or two curved hoses upward, over the appropriate tank edge, and toward a plausible intake, return, or aerator position.
* Include a few suction cups or clips. Hoses must connect to objects and respect glass boundaries.
* Use dark rubber or translucent tinted materials with restrained reflections.
* Place a small thermometer on the glass, with a backing, tick marks, and a colored indicator. It may be a decorative reading; do not present fabricated live sensor telemetry in the UI.
* Keep equipment and hoses clear of the open swimming area.

## 11. Mesh Net Leaning Beside the Cabinet

* Build a long handle, a thin rounded or oval frame, and a visible mesh bag.
* The bag must have an actual curved wire/grid structure; an empty hoop or opaque disk is insufficient.
* Use shared or merged line geometry for the netting instead of hundreds of separate meshes.
* Lean the net at a believable angle, with its lower end resting on the floor and the handle or rim near the cabinet.

## 12. Crooked Framed Fish Diagram

* Put a slightly tilted frame on the back wall with a locally drawn fish study or naturalist diagram.
* Include a border, paper surface, simple species text, and a recognizable clownfish outline with bands.
* Suitable text: `FIELD NOTES`, `Amphiprion ocellaris`, and `Plate 03 / The reef`.
* Generate the sketch and text from code. Do not fetch or embed an external illustration.

## 13. Stool, Yarn Ball, and Loose Thread

* Add a small stool beside or partly underneath the counter, with a seat, several legs, and support braces.
* Keep it physically separate from the cat and cabinet. No stool legs floating above the floor.
* Place a small yarn ball nearby with visible curved strands or wraps and a loose thread resting on the floor.
* The thread should follow a slightly irregular curve and stop naturally, rather than disappearing through the floor.

---

# Milo — Required Animated Cat Outside the Aquarium

Milo is a recognizable, slightly stylized tabby seated on the right countertop. Keep the cat in the default composition and close enough to reach the outside of the tank without stretching impossibly.

## Model and Articulation

Use a `THREE.Group` hierarchy with separate body, head, ears, eyes, muzzle, front paws, and tail components.

Include:

* A seated body with shoulders, haunches, and properly planted paws.
* Muted gray-brown tabby fur with procedural stripes and a lighter chest, muzzle, and paws.
* Two triangular ears with inner-ear color, a small nose, mouth, and fine whiskers.
* Two visible eyes, narrow pupils, and small highlights.
* A curved tail that can curl or flick independently.
* One articulated front paw that can lift toward the glass.

A plain sphere with ears is insufficient. Use combined ellipsoids, tapered shapes, curves, or custom geometry to establish a recognizable cat silhouette.

Document Milo's local forward axis separately from the fish axis, then consistently convert between local and world space for tracking and contact.

## Idle Behavior

* Add subtle breathing that does not slide the paws across the countertop.
* Blink occasionally with a short, natural closing-and-opening motion.
* Move the tail slowly, with a little more motion at its tip.
* Track the nearest fish with smooth, limited head yaw and pitch.
* Occasionally glance toward the camera, so the viewer can discover the eyes and expression.
* Keep the head, ears, paw, and tail free of obvious self-intersections and collisions with the tank or equipment.

## Click and Glass-Contact Behavior

Clicking Milo starts a short sequence:

1. Briefly glance toward the viewer.
2. Turn back toward the aquarium and raise one front paw.
3. Reach a physically plausible point on the **outside** of the nearest glass panel.
4. Produce a small circular highlight aligned with that panel's actual surface normal.
5. Nearby fish turn away briefly using their existing steering system.
6. Lower the paw and return to watching the fish.

Allow an occasional autonomous version of this action, roughly once every 20–45 seconds. Use a shared glass-tap cooldown, and let fish return to normal behavior promptly.

The paw contact and fish reaction must be connected events. Do not play unrelated animations or place the ripple on the front panel when the paw touches a side panel. Keep the body supported by the countertop throughout the sequence; the cat must not float, pass through the counter, or reach through the glass.

---

# Surface Wear and Controlled Imperfections

Add localized, believable signs of use to both the aquarium and the room:

* Faint algae patches around lower glass edges or selected corners.
* An irregular mineral line close to the water surface.
* A few small droplets on the outside of the front or side glass.
* A faint snail trail following the moving snail's recent path on the glass, using a fixed-length buffer or another bounded representation.
* Cabinet paint worn at corners and around handles.
* Directional wood scratches and slightly varied plank colors and joints.
* A small chip in the mug and terracotta pot.
* Cup rings, a few dried drips, and a rumpled cleaning cloth.
* A slightly crooked framed print and an uneven paper note.
* Loose food flakes, several escaped gravel pieces, and a mildly tangled cord.

Use geometry, vertex colors, shader noise, or textures generated inside the file. Vary scale and placement deliberately; do not stamp the same mark evenly across every object.

Keep the central viewing area of the glass mostly clear. Wear must not create a green opaque rectangle, hide the clownfish, flatten the lighting, or make the water look abandoned. Imperfection should reward a closer look while the whole scene remains attractive.

---

# Aquarium Construction

## Glass Panels

Build the aquarium from five individual glass panels:

* Front wall.
* Back wall.
* Left wall.
* Right wall.
* Bottom panel.

Do not place glass over the open top.

Use `MeshPhysicalMaterial` with values near:

```js
{
  color: 0xdffaff,
  transmission: 0.95,
  transparent: true,
  opacity: 0.16,
  roughness: 0.04,
  metalness: 0,
  thickness: 0.18,
  ior: 1.45,
  side: THREE.DoubleSide
}
```

The glass should have:

* Visible highlights along its edges.
* Slight cyan-green tint.
* Reflections from the aquarium lamp.
* Enough transparency that all decorations remain readable.
* Correct render ordering or material depth settings to minimize transparency artifacts.

Add thin bevel-like edge strips or narrow metallic/glass rods at the corners so the tank silhouette is clearly visible.

## Frame and Lamp

Add a dark matte frame around:

* The top perimeter.
* The bottom perimeter.
* Optionally the four vertical corners.

Use a nearly black material with slight roughness.

Above the water, create a slim aquarium lamp:

* Black rectangular housing.
* Thin glowing strip underneath.
* Warm white central light.
* Faint cool-blue secondary light.

The lamp should look like a real physical fixture, not just a floating point light.

---

# Water

Create a transparent water volume slightly smaller than the inner tank dimensions.

Suggested material:

* Blue-cyan tint.
* Opacity around `0.10–0.18`.
* High transparency.
* Low roughness.
* Optional slight transmission.

Do not make the water so opaque that the scenery becomes difficult to see.

## Animated Water Surface

Create a separate top water surface using a subdivided `PlaneGeometry`.

Animate its vertices or use a custom shader with multiple overlapping sine waves:

```text
wave =
    sin(x * frequencyA + time * speedA) * amplitudeA
  + sin(z * frequencyB + time * speedB) * amplitudeB
```

The water surface should:

* Ripple gently.
* Distort reflected light.
* Remain subtle.
* Move more strongly when the user drops food into the water.
* Have specular highlights from the lamp.

Add a faint bright waterline around the inside of the aquarium.

---

# Ground and Substrate

The aquarium floor must not be flat or empty.

## Layered Substrate

Create a layered substrate with:

1. A dark soil base.
2. A visible band of small pebbles.
3. A top layer of pale sand.

Use hundreds of lightweight procedural gravel particles, instanced meshes, or merged geometry where possible.

Suggested colors:

* Dark soil: `#33251e`
* Warm sand: `#c9ad7c`
* Beige gravel: `#a68b68`
* Gray gravel: `#77736c`
* Dark stones: `#47423c`

Give the terrain a slightly uneven profile:

* A low mound in one back corner.
* A shallow valley through the center.
* Sand accumulated around rocks and ruins.
* Small open swimming areas near the front.

Create a few subtle ripple patterns in the sand using curved ridges or thin torus segments.

---

# Main Environmental Focal Point

The aquarium should contain a strong central composition rather than randomly scattered objects.

## Giant Sea Anemone

Create a large sea anemone near the center-left or center-right.

The anemone should be the main home of the clownfish.

Build it procedurally from:

* A rounded organic base.
* Approximately 30–60 tentacles.
* Tentacles made with tapered cylinders, curves with `TubeGeometry`, or chains of small segments.
* Slight variation in length, thickness, color, bend, and animation phase.

Suggested colors:

* Base: muted violet, burgundy, or deep coral.
* Tentacle tips: pink, orange, cream, or fluorescent green.
* Slight emissive tint at the tips.

Animate every tentacle independently with slow underwater swaying.

At least one clownfish should occasionally circle, inspect, or briefly hide within the anemone.

The fish must not permanently disappear inside it.

---

# Large Decorative Props

Include at least four major decorative props.

## 1. Twisted Driftwood Arch

Create a procedural driftwood structure using several branching curved tubes.

It should:

* Form an arch or tunnel.
* Have uneven branches.
* Use dark brown rough material.
* Be partially buried in the sand.
* Have small plants or moss attached.
* Provide a path that fish can occasionally swim through.

Do not use a single plain cylinder.

## 2. Miniature Sunken Temple Ruins

Create a small ancient ruin in one back corner.

Possible elements:

* Two broken columns.
* A cracked stone arch.
* A tilted slab.
* Small staircase.
* Fragment of a statue head.
* Moss growing over some surfaces.

Use procedural box, cylinder, torus, and custom broken-shape geometry.

Suggested stone colors:

* `#6e7772`
* `#818b82`
* `#59645d`

Add edge wear through layered geometry or color variation.

The ruin should look weathered and partially buried, not like clean primitives.

## 3. Treasure Chest with Bubble Surprise

Place a small half-buried treasure chest near the driftwood or ruins.

Construct it from:

* A dark wooden box.
* Curved lid.
* Metal bands.
* Small lock.
* A few visible gold coins or glowing pearls.

Animate the lid so that it opens slightly every 12–20 seconds, releases a burst of bubbles, then closes again.

The motion should be subtle and charming, not cartoonishly fast.

Add a faint warm golden glow from inside while the lid is open.

## 4. Sunken Glass Bottle

Add a tilted transparent bottle partially buried in the sand.

Inside the bottle, place either:

* A tiny rolled message.
* A miniature glowing object.
* A tiny procedural ship silhouette.

The bottle should create a hidden discovery when the camera is rotated.

Use simple glass geometry and avoid severe transparency artifacts.

---

# Additional Decorative Details

Scatter smaller details around the environment to make it feel handcrafted.

Include several of the following:

* Small coral branches.
* Mushroom-shaped coral.
* Shells.
* Starfish on the sand or glass.
* A tiny ceramic diver helmet.
* A broken anchor.
* A small skull-shaped rock, stylized rather than frightening.
* A miniature “No Fishing” sign.
* One rubber duck ornament partially hidden behind plants.
* Tiny glowing pearls near the treasure chest.
* Moss patches on the ruins.
* Thin roots growing around rocks.
* A small cave under the driftwood.
* A crab burrow entrance.
* Pebbles stacked into a tiny balancing tower.

Do not arrange everything evenly. Use intentional clusters and leave some negative space.

At least one humorous detail should be partially hidden and only noticeable from certain camera angles.

---

# Rocks and Gravel

Add:

* 20–35 medium decorative stones.
* Numerous small gravel pieces.
* 3–5 larger feature rocks.

Use a mixture of:

* `DodecahedronGeometry`
* `IcosahedronGeometry`
* Distorted `SphereGeometry`
* Custom vertex noise

Randomize:

* Scale.
* Rotation.
* Flattening.
* Roughness.
* Color.
* Partial burial depth.

Avoid perfect spheres.

Create one larger rock cave or overhang where fish can swim nearby.

---

# Aquatic Plants

Create 6–9 plant clusters with visual variety.

Do not make every plant from identical vertical green planes.

## Plant Type A: Tall Ribbon Grass

* Long narrow blades.
* Back corners and rear wall.
* Dark green base.
* Brighter translucent tips.
* Gentle independent swaying.

## Plant Type B: Broad-Leaved Plant

* Larger oval or lance-shaped leaves.
* Short stems.
* Positioned near rocks or driftwood.
* Slower movement.

## Plant Type C: Red Accent Plant

* Burgundy, orange-red, or deep purple leaves.
* Use only in one or two clusters as a visual accent.

## Plant Type D: Moss

* Small clumps attached to wood and ruins.
* Constructed from clusters of small soft shapes.

Every plant should have a randomized animation phase so the scene does not sway uniformly.

The animation should appear strongest near leaf tips and minimal near roots.

---

# Coral

Add several stylized procedural coral formations:

* Branching coral using recursive tapered cylinders.
* Rounded brain coral using a distorted sphere with ridge-like curves.
* Small tube coral with multiple hollow cylinders.
* Soft coral with animated curved branches.

Use restrained colors:

* Coral orange.
* Muted pink.
* Pale lavender.
* Warm cream.
* Deep red accents.

Avoid turning the aquarium into a neon rainbow.

Use emissive material only very subtly.

---

# Clownfish

Create three detailed procedural clownfish inspired by **Amphiprion ocellaris**.

The fish must be recognizable from their body silhouette and coloration.

They must not look like plain stretched spheres.

## Required Fish Structure

Each fish must be a hierarchy based on `THREE.Group`, with separate animated components.

### Body

Use one of these approaches:

* Custom `LatheGeometry`.
* Distorted high-segment sphere.
* A body assembled from overlapping ellipsoids.
* A custom parametric geometry.

The shape should include:

* Rounded head.
* Fuller central body.
* Narrow caudal peduncle near the tail.
* Slightly flattened sides.
* Curved belly.
* Taper toward the tail.

Suggested orientation:

* Fish forward direction should follow a clearly documented local axis.
* All movement and turning calculations must use the same axis consistently.

### Clownfish Pattern

Add:

* Bright orange body.
* Three white vertical bands.
* Thin black borders around the white bands.
* Dark edging around fins.
* Slightly pale belly.

The stripes should follow the body volume.

Preferred approaches:

1. A custom shader based on local body coordinates.
2. Closely fitted stripe shell geometries.
3. Segmented body sections with no obvious gaps.

Do not place flat rectangular stripes through the fish body.

### Head and Face

Include:

* Two eyes.
* Dark pupils.
* Small glossy highlight dots.
* Slightly raised eye sockets.
* Small mouth.
* Optional cheek contour.

The fish should look lively, but not overly cartoonish.

### Tail

Create a rounded fan-shaped tail from `ShapeGeometry` or thin `ExtrudeGeometry`.

The tail must:

* Wag continuously.
* Bend more strongly while accelerating.
* Slow slightly when hovering.
* Have black edging.
* Optionally contain an orange-to-transparent gradient approximation.

### Fins

Each fish must include:

* One dorsal fin.
* Two pectoral fins.
* One anal fin.
* Optional small pelvic fins.

Animate:

* Tail wagging.
* Pectoral fin flapping.
* Slight dorsal fin sway.
* Small full-body undulation.

## Fish Variation

Use sizes near:

* Fish 1: `0.88`
* Fish 2: `1.0`
* Fish 3: `1.12`

Also vary:

* Orange hue.
* Stripe width.
* Fin size.
* Swimming speed.
* Preferred aquarium zone.
* Personality.

Possible personalities:

* Curious fish: approaches the front glass and follows food.
* Shy fish: stays near the anemone and ruins.
* Explorer fish: swims through the driftwood arch and around the entire tank.

---

# Fish Movement and Behavior

Implement autonomous movement using smooth waypoint navigation or lightweight steering behavior.

Each fish should:

* Choose reachable target positions within safe tank bounds.
* Smoothly accelerate and decelerate.
* Turn gradually using quaternion interpolation.
* Bank gently during turns.
* Bob slightly while swimming.
* Avoid glass walls.
* Avoid the floor and water surface.
* Avoid passing directly through large decorations.
* Maintain some separation from other fish.
* Occasionally pause or hover near a plant, rock, or anemone.
* Occasionally swim through the driftwood arch.
* React to food particles.
* React briefly to a nearby glass tap, including a tap initiated by Milo outside the tank.

Do not use abrupt direction changes.

## Boundary Avoidance

Use soft steering forces near boundaries rather than only clamping positions.

Fish should begin turning before reaching the glass.

Maintain a safe margin from:

* Front and back walls.
* Side walls.
* Sand.
* Water surface.

## Decorative Object Avoidance

Represent large objects with simplified bounding spheres or boxes:

* Anemone base.
* Driftwood.
* Temple ruins.
* Large rocks.
* Treasure chest.

Fish should steer around these volumes.

Perfect collision detection is unnecessary, but obvious clipping must be avoided.

## Social Behavior

Add lightweight schooling behavior:

* Separation when fish are too close.
* Mild alignment when nearby.
* Occasional following.
* No rigid synchronized formation.

## Anemone Behavior

At random intervals, one fish should:

* Approach the anemone.
* Slow down.
* Circle it once.
* Hover among the tentacles briefly.
* Return to normal roaming.

---

# Small Living Creatures

Add at least two small secondary creatures.

## Snail

Create a small snail moving very slowly across:

* A rock.
* The aquarium glass.
* Or the ruins.

Include:

* Spiral shell.
* Small body.
* Two antennae.

Movement can be extremely slow but should be visible over time.

## Cleaner Shrimp

Create one small shrimp near a rock or anemone.

Use:

* Segmented translucent body.
* Long antennae.
* Tiny animated legs.
* Gentle idle motion.

The shrimp does not need advanced navigation.

Optionally make it retreat slightly when a fish approaches.

## Optional Tiny Crab

A very small crab may occasionally:

* Emerge from a burrow.
* Walk sideways a short distance.
* Hide again.

Keep it simple and low-poly.

---

# Bubble Systems

Create several types of bubbles.

## Continuous Aerator Stream

Place a small air stone behind a rock.

Spawn approximately 2–4 bubbles per second.

Bubbles should:

* Rise at slightly different speeds.
* Wobble horizontally.
* Vary in size.
* Expand slightly near the surface.
* Disappear at the waterline.
* Recycle through an object pool.

## Treasure Chest Bubble Burst

Whenever the treasure chest opens:

* Release 8–16 bubbles.
* Use slightly larger bubbles.
* Apply randomized outward velocities.
* Fade them near the surface.

## Microbubbles

Add a small number of tiny slow particles suspended in the water.

They should drift with the current and create a sense of water volume.

---

# Suspended Particles and Plankton

Create a lightweight particle system inside the tank with:

* Tiny dust-like particles.
* Slow vertical and horizontal drift.
* Different depths.
* Very low opacity.
* Occasional faint glow.

Add a few subtle bioluminescent plankton particles that brighten briefly at random.

Keep the effect elegant and sparse.

The particles should make the water feel deep while preserving clear visibility. Localized algae and mineral wear belong to the glass surfaces, not an opaque cloud filling the tank.

---

# Caustics and Underwater Lighting

Create procedural moving caustic effects without image textures.

Possible implementation:

* Transparent animated planes projected near the sand.
* Shader-generated moving wave patterns.
* Several overlapping soft spotlights or projected mesh patterns.
* Additive transparent polygons moving slowly across the floor.

The caustics should:

* Move slowly over sand, rocks, ruins, and fish.
* Be strongest below the lamp.
* Remain subtle.
* Avoid obvious repeating stripes.
* Apply strong underwater caustics only inside the tank bounds. Do not accidentally shade Milo, the mug, or the cabinet as though they were underwater.

---

# Lighting Setup

Use a cinematic multi-light setup.

## Ambient Light

Soft blue-white fill:

```js
new THREE.AmbientLight(0xb3e5fc, 0.35)
```

## Hemisphere Light

Add a hemisphere light:

* Sky: pale blue.
* Ground: deep teal or dark brown.
* Low-to-medium intensity.

## Main Aquarium Lamp

Use one or two lights under the lamp housing:

* Warm-white central light.
* Slightly cool fill light.
* Soft shadows.

## Directional Key Light

Place a directional light above and in front of the tank.

Use:

* Warm-white color.
* Medium intensity.
* Soft shadow map.
* Shadow camera bounds sized for the full keeper's corner, including the cabinet, cat, and floor. Keep shadows stable and reasonably sharp at the aquarium scale.

## Accent Lights

Add subtle accent lighting:

* Weak cyan light from one side.
* Very faint golden glow from the treasure chest.
* Soft emissive anemone tips.
* Optional dim violet light behind the ruins.

## Room Lighting

* Add a warm practical light under the desk-lamp shade that affects nearby objects.
* Balance it with cool window and aquarium fill so the cat, cupboard, and tools remain readable.
* The window gradient, lamp brightness, aquarium lighting, and emissive accents transition together when the shared Day/Night state changes.
* Create reflections with a procedurally generated environment if needed; no external HDR file.

Do not overexpose the fish, turn the glass completely white, or lose the entire exterior scene in darkness.

---

# Shadows and Rendering

Enable:

```js
renderer.shadowMap.enabled = true;
renderer.shadowMap.type = THREE.PCFSoftShadowMap;
renderer.toneMapping = THREE.ACESFilmicToneMapping;
renderer.toneMappingExposure = 1.1;
renderer.outputColorSpace = THREE.SRGBColorSpace;
```

Use shadow casting selectively:

* Fish.
* Large rocks.
* Driftwood.
* Ruins.
* Treasure chest.
* Major plants.
* Milo and the larger exterior props.
* Countertop, cabinet, stool, and selected window or lamp components.

Avoid enabling shadows on hundreds of tiny gravel objects if it damages performance.

Use instancing or merged geometry for repeated small elements.

Set the renderer pixel ratio to:

```js
Math.min(window.devicePixelRatio, 2)
```

to avoid excessive GPU load on high-density displays.

---

# Camera and Controls

Use `OrbitControls` with damping, left-drag orbit, wheel zoom, right-drag pan, and touch support. Constrain polar angle, zoom, and pan so ordinary use does not lose the scene or move below the floor.

## Required Room View

The initial camera shows a cinematic three-quarter view of the **complete keeper's corner**: tank, cabinet, floor edge, window, desk objects, Milo, net, and stool. The aquarium remains the main focal point, and Milo is recognizable beside it.


Leave a small visual margin around primary objects. Check the open cabinet-door pose and Milo's raised paw as well as the resting scene.

## Required Reef View

Provide a smooth transition to a closer three-quarter view of the aquarium. This view makes fish, anemone tentacles, coral, glass wear, and small discoveries easy to inspect.

Animate both the camera position and the orbit target. Keep the same world and controls; do not swap to an unrelated flat illustration or remove the room objects.

The view button reads `Reef view` while in Room view and `Room view` while in Reef view. `Reset camera` returns to the default Room view.

## Responsive Framing and Idle Motion

* Recompute the fitted camera distance and target when the viewport size changes.
* Ensure `controls.maxDistance` allows the computed fit distance. Do not let OrbitControls continuously clamp a camera-reset animation before it reaches its target.
* Prevent horizontal page overflow and clipped controls on narrow screens.
* Add a very subtle idle drift only after several seconds without interaction. Stop it immediately during pointer interaction and while the simulation is paused.
* Respect reduced-motion preferences by disabling idle camera drift and shortening nonessential interface transitions.
* Make the back wall a practical cutaway or selectively visible surface so orbiting around the scene remains useful.

---

# User Interaction

Use meaningful interactions connecting the room and the aquarium. All actions below require their visible animation or simulation effect, not merely a message.

## Shared Interaction Map

| Trigger | Required visible result |
|---|---|
| Click the water surface or double-click inside the tank | Drop 8–15 food particles at a safe world position, create a surface ripple, attract fish, and let fish eat pellets. |
| Click `Feed fish` | Use the same food system at a sensible default location. |
| Click the real food jar | Briefly shake the jar and lid, then use the same feeding system and cooldown. |
| Click front or side glass | Create a small highlight aligned with the hit surface; nearby fish turn away briefly. |
| Click Milo | Glance, raise a paw, touch the actual glass surface, trigger a nearby fish reaction, and settle back down. |
| Click the treasure chest | Open early, release a bounded bubble burst, increase the interior glow, and close again. |
| Click the hidden rubber duck | Bob or rotate it once, then return it to its resting pose. |
| Click the cabinet door | Open or close it around its hinge, revealing the modeled storage contents. |
| Click the notebook | Lift or turn a real page around the spine, then let it settle. |
| Click the desk lamp or Day/Night button | Update one shared lighting state with a smooth transition, including the room and aquarium. |

## Food Behavior

Food particles sink slowly, drift horizontally, and attract nearby clownfish. Fish temporarily change their targets, approach smoothly, and nibble a reachable particle. Remove eaten or expired food. Use a fixed maximum count and a cooldown of roughly 2–3 seconds across every feeding entry point.

Keep food inside the tank and under the waterline. Clicking a jar outside the aquarium must not spawn pellets on the countertop or make fish leave the tank to reach it.

## Accurate Picking and Animation State

* Calculate pointer coordinates relative to the actual canvas bounding rectangle.
* Distinguish a drag from a click using a small movement threshold. Orbiting must not accidentally feed fish or activate room objects.
* Disambiguate single and double clicks so a double-click does not accidentally cause two independent actions.
* Use correctly positioned raycast targets or proxies that follow their parent objects when a door, cat, or lid moves.
* Resolve the nearest eligible object. Transparent aquarium glass may allow picking an intended underwater object, but opaque room geometry must not allow arbitrary click-through activation of hidden objects.
* Use the world-space hit point and normal to orient a glass-tap highlight. Front and side panels require different orientations.
* Use bounded states and shared cooldowns for repeated actions; do not accumulate timers, meshes, event handlers, or overlapping door animations.

## Discoverability

Use a pointer cursor and a small hover hint for clickable props where appropriate. A short toast can acknowledge an action without obscuring the scene. Hover is a supplement; the main controls remain usable on touch screens.

Show an initial hint such as:

```text
Drag to explore • Scroll to zoom • Double-click the water to feed • Try the cat and the room objects
```


---

# Required Interface and Day/Night State

Use plain HTML and CSS with a compact, translucent control dock. Provide:

* `Feed fish`.
* `Day / Night`.
* `Pause / Resume`.
* `Reef view / Room view`.
* `Reset camera`.
* `Hide UI`, plus a recoverable `Show controls` button or keyboard shortcut.

Use accessible names, keyboard focus styles, and correct pressed states. Suggested shortcuts are F for feeding, N for lighting, Space for pause, C for view, R for reset, and H for optional UI visibility.


## Day Mode

* Clearer blue water, warm aquarium illumination, and visible but restrained caustics.
* A warm pool of light around the real desk lamp.
* Readable walnut grain, cabinet paint, paper, mug, and Milo.
* A muted procedural daytime view through the window.

## Night Mode

* A darker navy environment and window, with a procedural moon.
* Dimmer aquarium light and brighter-looking anemone tips and plankton.
* A slightly stronger relative treasure glow.
* Retain enough warm practical light and cool fill to read the room and cat; avoid an entirely black exterior.

Transition shared lighting parameters over roughly 1.5–3 seconds. Clicking the desk lamp and clicking the UI button must keep the same state, label, and pressed value.

## Pause and UI Visibility

Pause freezes the simulation: fish, fins, vegetation, bubbles, food, water, caustics, snail, shrimp, chest, Milo, steam, clock hands, and active prop motion. Camera orbit and UI controls remain usable. Day/Night and camera-view transitions may still operate while the living simulation is paused.

An explicit feeding or prop-animation action may resume the simulation automatically, but it must also update the Pause/Resume button and status correctly. Passive hovering does not resume it.


---

# Animation Requirements

Use **one central `requestAnimationFrame` loop** with delta time from `THREE.Clock`, a shared simulation time, and explicit animation states.

Update the following from that loop:

* Fish steering, acceleration, turning, banking, tail motion, fins, and subtle body undulation.
* Plant swaying, independent anemone tentacles, and soft coral.
* Water waves, feed ripples, glass-tap highlights, and caustics.
* Pooled bubbles, chest bursts, food, suspended particles, and plankton.
* Snail movement and its bounded trail, shrimp legs, and any crab behavior.
* Chest lid and interior light.
* Milo's breathing, head tracking, glances, blink, tail, paw sequence, and synchronized fish reaction.
* Gently moving houseplant leaves and rising, fading mug steam.
* Wall-clock hands, hinged cabinet door, food-jar shake, and notebook page.
* Smooth shared lighting transitions and camera-view transitions.
* Limited idle camera movement when allowed.

Movement must be frame-rate independent wherever practical. Use delta time and exponential damping or equivalent time-based interpolation, not unscaled fixed-per-frame increments.

Clamp unreasonable delta-time jumps after a background tab resumes. Keep simulation time separate from interface-transition time so Pause behaves consistently. Reset or recover the frame loop correctly after a WebGL context loss.

---

# Performance Strategy

Maintain a rich underwater world and furnished room without thousands of independent draw calls.

Use:

* Instanced meshes for gravel, repeated stones, droplets, and suitable repeated tail or decorative elements.
* Shared geometries and a restrained material palette.
* Material-based merging for static room furniture and decorations.
* Separate moving groups for fish components, Milo's head and paw, cabinet door, chest lid, and notebook page.
* Batched line geometry for netting, whiskers, cords, or trails where appropriate.
* GPU vertex deformation or lightweight reusable buffers for plants, tentacles, and water.
* Fixed-size pools for food, bubbles, steam, ripples, and trails.
* Moderate segment counts, simple collision proxies, selective shadows, and pixel ratio capped at 2.
* Procedural textures created once at initialization and reused, with appropriate color space.

When merging geometry, preserve the attributes needed by each material, especially UVs for generated labels, vertex colors, and custom deformation attributes. Do not flatten independently animated children into a static batch. Keep raycast proxies attached to their moving parents.

Avoid rebuilding and disposing of full tube, tail, or plant geometries every frame. Reuse buffers, joint transforms, or instancing. Avoid allocating large arrays in the animation loop.

Keep transparent layers sparse, order them carefully, and avoid unnecessary depth writing or double rendering where a simpler material is sufficient. Keep the main glass readable when droplets, algae, water, and the snail trail overlap.


Dispose of generated textures, geometries, materials, render targets, controls, and listeners when the application is actually torn down.

---

# Code Structure

Organize the JavaScript into clear sections, factories, or classes:

1. Renderer, scene, shared state, and dependency initialization.
2. Materials, procedural textures, label drawing, and batching helpers.
3. Camera fitting, Room/Reef transitions, and OrbitControls.
4. Room and aquarium lighting with one shared Day/Night state.
5. Aquarium glass, frame, lamp, water volume, and surface.
6. Terrain, substrate, rocks, and underwater decorations.
7. Plants, coral, and anemone deformation.
8. Clownfish factory, steering, boundaries, and object avoidance.
9. Secondary creatures and snail trail.
10. Room floor, wall, cabinet, window, and furniture.
11. Desk objects, notebook, mug, food jar, care equipment, and wear.
12. Milo's model, head tracking, blink, tail, paw state, and fish reaction.
13. Food, bubbles, steam, particles, and other pools.
14. Raycasting, click/drag discrimination, shared actions, and UI.
15. One central animation loop and pause semantics.
17. Resource cleanup.

Use descriptive names and comments. Keep model construction separate from per-frame updates. Document local coordinate conventions and moving pivots. Avoid putting the entire application inside one unreadable function.

---

# Visual Composition Guidelines

Build two connected compositions that work together from the default angle.

## Inside the Glass

* Place the large anemone slightly off-center, opposite the driftwood arch.
* Put the ruins in a rear corner, with moss and taller plants around them.
* Tuck the chest beside or under the driftwood and place the bottle toward a front side.
* Use restrained coral clusters to connect major props.
* Keep an open front sand path and enough midwater space for all three fish.
* Hide the air stone and rubber duck partially, while leaving side-view discoveries.
* Keep algae and mineral wear concentrated at edges rather than over the main viewing area.

## Around the Glass

* Anchor the tank to its plinth, countertop, cabinet, and floor with convincing contact and shadows.
* Balance the window, houseplant, and desk lamp on the left with Milo, the filter, and net on the right.
* Use the jar, open notebook, cloth, mug, and a few spills to make the front ledge feel used.
* Keep the jar visibly outside the glass and within easy reach of the pointer.
* Leave enough clear space for Milo's body, tail, and paw. A stool below the counter must not intersect the cat.
* Use the clock, crooked study print, cabinet note, open shelf, and yarn as secondary discoveries.
* Vary alignment, rotation, material wear, and clustering without losing a coherent palette.

## Screen Composition

The default Room view shows the main diorama without cropping its floor edge, cabinet, lamp, or cat. Reef view intentionally brings the tank closer for inspection.


Aim for an attractive screenshot that already communicates a miniature living reef and the life around it, with more detail revealed through interaction.

---

# Quality Priorities

The mandatory requirements are not optional stretch goals. If a detail is expensive, simplify its geometry or shader while preserving its identity and behavior.

Prioritize:

1. A stable, working single HTML file with correct imports and no runtime or shader errors.
3. Three recognizable animated clownfish with natural motion and containment.
4. A lush, varied aquarium with its required anemone, plants, coral, rocks, ruins, wood, chest, and bottle.
5. The furnished exterior, recognizable animated Milo, and interactions that connect room objects to the aquarium.
6. Clear glass, animated water, coherent day/night lighting, and selective soft shadows.
7. Feeding, bubbles, secondary creatures, steam, glass wear, and smaller discoveries.
8. Fine surface detail, humorous notes, and subtle finishing touches.


---

# Acceptance Criteria

The result succeeds only when all mandatory groups below pass.

## Packaging and Stability

* Exactly one complete HTML file contains the CSS, JavaScript, shaders, and runtime-generated art.
* Compatible CDN imports resolve correctly, including the bare `three` imports used by addons.
* There are no console errors, broken assets, shader compilation errors, or invalid geometry.
* The central animation loop starts and resize handling works.


## Aquarium

* Three recognizable clownfish have orange bodies, three fitted white bands with black borders, eyes, mouths, tails, and fins.
* Tails and fins animate; fish move autonomously, turn smoothly, stay inside the tank, and avoid constant clipping through major props.
* The interior contains layered substrate, gravel, rocks, varied plants, multiple coral types, a swaying anemone, driftwood, ruins, chest, bottle, bubbles, and smaller details.
* Water ripples and caustics animate; transparent layers leave the interior readable.
* Tentacles and plants have independent motion phases.
* The chest periodically opens, glows, emits bubbles, and closes.
* At least the snail and cleaner shrimp are present and visibly animated; the glass snail leaves a bounded, faint trail.
* Feeding from the water, button, and food jar produces actual food that fish approach and eat.

## Exterior and Milo

* Room view visibly includes the modeled cabinet, countertop, floor, back wall, window and blinds, desk lamp, houseplant, mug, food jar, notebook, cleaning cloth, equipment, net, framed study, clock, books, stool, and yarn detail.
* The cabinet door opens around a hinge to reveal real supplies.
* The mug emits subtle steam, clock hands advance, and room-plant leaves move gently.
* The jar and its lid animate when clicked; the notebook has an actually moving page.
* Milo is recognizable, sits on a valid supporting surface, blinks, breathes, tracks fish, glances toward the viewer, and moves his tail.
* Clicking Milo produces a believable paw-to-glass contact and a brief nearby fish reaction, then returns to idle.
* The cat, cupboard, tools, hoses, and tabletop do not visibly intersect in their primary resting and animated poses.
* Wear, chips, rings, spills, algae, droplets, and uneven placement make the corner feel used without obscuring the scene.

## Interaction, Framing, and Performance

* Orbit, zoom, constrained pan, and both camera views work.
* Dragging does not accidentally activate feeding or room props.
* Clicks use correct pointer coordinates, attached hit targets, and panel normals.
* The desk lamp and UI Day/Night control stay synchronized.
* Pause freezes the simulation coherently while camera and interface controls remain usable.
* Room view fits the primary diorama and reserves space for the large heading and dock.
* Pools remain bounded after repeated feeding, chest opening, and cat interaction. Repeated actions do not continuously increase object counts.
* The scene remains smooth on a modern desktop, visually coherent, alive, playful, and worth exploring.

---

# Final Output Instructions

Return only the complete HTML code inside a single code block.

Do not provide explanations before or after the code. Do not provide multiple files, external art assets, or build instructions as substitutes for the working HTML.

Do not use placeholders such as “Add fish here,” “Implement the cat later,” “Room decorations omitted,” “Rest of code omitted,” “Use your own shader,” or “Insert geometry.”


Before producing the final answer, internally verify:

* All imports use compatible Three.js versions and resolve through a valid module setup.
* Every referenced variable, function, uniform, material, and geometry exists and is valid.
* The single frame loop starts, object pools are bounded, and pause/resume is coherent.
* Resize handling fits the full room and close tank views without fighting OrbitControls limits.
* Transparent objects do not hide the aquarium interior; underwater caustics are confined to the water's region.
* Fish orientation matches their movement direction, and the main decorations have usable avoidance proxies.
* Milo's local/world transforms place the paw on the actual glass, with the contact highlight using the correct normal.
* Food from the exterior jar enters the tank, and the fish can reach and eat it.
* The cabinet door, notebook page, chest lid, and cat remain properly articulated and do not become static during batching.
* Generated text textures retain their UVs and remain readable when viewed closely.
* Labels, hints, and toasts supplement visible behavior rather than replacing it.
* The room, lighting, wear, and underwater composition still look intentional at the default camera angle.

---

НЕ ЗАПУСКАЕШЬ СУБАГЕНТОВ, НЕ ПОДГЛЯДЫВАЕШЬ КАК ДРУГИЕ AI СДЕЛАЛИ АКВАРИУМ, В ДРУГИХ ПАПКАХ! ВСЁ САМ! И БЕЗ PLAN МОДА. ПРОСТО ДЕЛАЙ

