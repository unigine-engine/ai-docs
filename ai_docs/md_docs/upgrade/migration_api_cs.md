# API Migration (CS)


## Major Changes


- Added a new *[GlobalConfig](../api/library/engine/class.globalconfig_cs.md)* class.
- Added a new *[DataBridge::Manager](../api/library/plugins/databridge/class.databridge_manager_cs.md)* class.
- Added a new *[DataBridgeUI](../api/library/plugins/databridge/class.databridgeui_cs.md)* class.
- Added a new *[DBVariable](../api/library/plugins/databridge/class.dbvariable_cs.md)* class.
- Added a new *[NetworkInstance](../api/library/plugins/databridge/class.networkinstance_cs.md)* class.
- Added a new *[NetworkManager](../api/library/plugins/databridge/class.networkmanager_cs.md)* class.
- Added a new *[Server](../api/library/plugins/databridge/class.server_cs.md)* class.
- Added a new *[Client](../api/library/plugins/databridge/class.client_cs.md)* class.
- Added a new *[Sql](../api/library/plugins/sql/class.sql_cs.md)* class.
- Added a new *[SqlDatabase](../api/library/plugins/sql/class.sqldatabase_cs.md)* class.
- Added a new *[SqlRequest](../api/library/plugins/sql/class.sqlrequest_cs.md)* class.
- Added a new *[SqlResponse](../api/library/plugins/sql/class.sqlresponse_cs.md)* class.
- Added a new *[PathWildcards](../api/library/common/class.pathwildcards_cs.md)* class.
- Added a new *[PDFFile](../api/library/plugins/pdfrender/class.pdffile_cs.md)* class.
- Added a new *[PDFRender::Manager](../api/library/plugins/pdfrender/class.pdfrender_manager_cs.md)* class.
- Added a new *[ProfilerDump](../api/library/engine/class.profilerdump_cs.md)* class.
- Added a new *[ThreadsPool](../api/library/common/mt/class.threadspool_cs.md)* class.
- Added a new *[AsyncTaskCallable](../api/library/common/mt/class.asynctaskcallable_cs.md)* class.
- Added a new *[CPUTask](../api/library/common/mt/class.cputask_cs.md)* class.
- Added a new *[Skeleton](../api/library/animations/skeletal/class.skeleton_cs.md)* class.
- Added a new *[SkeletonPoseDecomposed](../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* class.
- Added a new *[SkeletonPoseMatrix](../api/library/animations/skeletal/class.skeletonposematrix_cs.md)* class.
- Added a new *[SkeletonRetargeter](../api/library/animations/skeletal/class.skeletonretargeter_cs.md)* class.
- Added a new *[SkeletonRetargeterEquals](../api/library/animations/skeletal/class.skeletonretargeterequals_cs.md)* class.
- Added a new *[SkeletonRetargeterNamesMatching](../api/library/animations/skeletal/class.skeletonretargeternamesmatching_cs.md)* class.
- Added a new *[SkeletonRetargeterTranslations](../api/library/animations/skeletal/class.skeletonretargetertranslations_cs.md)* class.
- Added a new *[MeshSkinned](../api/library/rendering/class.meshskinned_cs.md)* class.
- Added a new *[MeshSkinnedAnimation](../api/library/rendering/class.meshskinnedanimation_cs.md)* class.
- Added a new *[NodeSkeletonPose](../api/library/nodes/class.nodeskeletonpose_cs.md)* class.
- Added a new *[AnimScript](../api/library/animations/skeletal/class.animscript_cs.md)* class.
- Added a new *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cs.md)* class.
- Added a new *[ImportSkeleton](../api/library/common/import/class.importskeleton_cs.md)* class.
- Added a new *[MediaPlayer::Manager](../api/library/plugins/mediaplayer/class.mediaplayer_manager_cs.md)* class.
- Added a new *[MediaPlayer::VideoSource Class](../api/library/plugins/mediaplayer/class.mediaplayer_videosource_cs.md)* class.
- Added a new *[VideoSourceComponent](../api/library/plugins/mediaplayer/class.videosourcecomponent_cs.md)* class.
- Renamed the *WorldTransformBone* class as *[WorldTransformJoint](../api/library/worlds/class.worldtransformjoint_cs.md)* class.
- Renamed the *BonesRetargeting* class as *[SkeletonRetargeter](../api/library/animations/skeletal/class.skeletonretargeter_cs.md)* class.
- The *ObjectMeshSkinned* class has been renamed as *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. A new simplified *[ObjectMeshSkinned](../api/library/objects/class.objectmeshskinned_cs.md)* class has been added.
- The *PoolCPUShaders* class has been removed.


### IG-Related Changes


- The *IG::Converter* class has been split into two classes: Due to this, the return value of *[IG::Manager::getConverter()](../api/library/plugins/ig/api/class.managerinterface_cs.md#getConverter_Converter)* has been changed to *Geodetics::Converter* to minimize manual migration, for cases related to axis conversions NED to ENU and ENU to NED, use the *[IG::Manager::getNEDConverter()](../api/library/plugins/ig/api/class.managerinterface_cs.md#getNEDConverter_NEDConverter)* method instead.

  - *[Geodetics::Converter](../api/library/geodetics/geodetics_plugin/class.converter_cs.md)* - the class of the *[Geodetics](../api/library/geodetics/geodetics_plugin/index.md)* plugin containing most methods of the former *IG::Converter* class.
  - *[IG::NEDConverter](../api/library/plugins/ig/api/class.nedconverter_cs.md)* - a new class containing methods for axis conversions NED to ENU and ENU to NED.
- The *GeodeticsTransformer* class has been moved to the *[Geodetics](../api/library/geodetics/geodetics_plugin/index.md)* plugin. Relevant changes include: | UNIGINE 2.20 | UNIGINE 2.21 | |---|---| | *`UnigineGeodeticsTransformer.h`* | Changed to `plugins/Unigine/Geodetics/UnigineGeodetics.h` | | ***UnigineGeodetics.h*** | Renamed to `UnigineGeodeticPivot.h` (the *[GeodeticPivot](../api/library/geodetics/class.geodeticpivot_cs.md)* class API is unchanged). | | Complex initialization process: ```cpp auto transformer = GeodeticsTransformer::get(); if (!transformer) { Log::warning("Can't get transformer\n"); return 0; } int epsg_code = 3857; // EPSG Geodetic Parameter Dataset code dvec3 geodetic_origin = dvec3_zero; dvec3 original_geo_pos = dvec3(35.105580, -89.966775, 0.0); dvec3 world_pos, geo_pos; // setup projection transformer->setProjectionEpsg(epsg_code, geodetic_origin); // geodetic to world world_pos = transformer->geodeticToWorld(original_geo_pos).getTranslate(); // world to geodetic geo_pos = transformer->worldToGeodetic(world_pos); ``` | Simpler initialization for a georeferenced world - a world having an enabled [Geodetic Pivot](../objects/geodetics/geodeticpivot/index.md) or a [Sandworm](../editor2/sandworm/index.md)-generated terrain: ```cpp Unigine::Math::dvec3 original_geo_pos = Unigine::Math::dvec3(35.105580, -89.966775, 0.0); Unigine::Math::dvec3 world_pos, geo_pos; world_pos = Unigine::Plugins::Geodetics::Converter::get()->geodeticToWorld(original_geo_pos); geo_pos = Unigine::Plugins::Geodetics::Converter::get()->worldToGeodetic(world_pos); ``` (previous complex approach is still valid) | | *Unigine::GeodeticsTransformer::get()* | Changed to *Unigine::Plugins::Geodetics::Transformer::get()* |
- The IG Weather classes (*SkyMap*, *Meteo*, *Water*, etc.) have been moved to the *Weather* plugin. Due to this, the return value of *[IG::Manager::getMeteo()](../api/library/plugins/ig/api/class.managerinterface_cs.md#getMeteo_Meteo)* has been changed to minimize manual migration.
- `ig_config.xml` has been split into two files: `ig_config.xml` and `weather_config.xml` - this is covered by automatic migration.
- File location of the IG content has been changed: previously the `ig_data/ig.umount` file, now it is stored as `data/modules/ig.ung` and `data/modules/weather.ung` - this is covered by automatic migration.


## Breaking Changes


### Removed Save() and Restore()


The methods ***Save()*** and ***Restore()*** have been removed from ***AppWorldLogic.cs***, similarly ***SaveState()*** and ***RestoreState()*** have been removed from *[*Unigine.Plugin*](../api/library/common/class.plugin_cs.md)* class. When migrating your project to 2.21, you need to manually remove these methods, otherwise your project will not compile.


## AsyncQueue Class


The *ASYNC_THREAD* enum values have been completely reordered. The *ASYNC_PRIORITY* enum has been expanded from 3 to 8 priority levels. Thread-checking methods have been renamed with a *Pool* prefix for consistency.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***ASYNC_THREAD.ASYNC_FRAME_POOL*** | Removed. |
| ***ASYNC_PRIORITY.DEFAULT*** | Removed. Use *[**ASYNC_PRIORITY.NORMAL**](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_PRIORITY_NORMAL)* instead. |
| ***IsGPUStreamThread**( )* | Renamed. Use *[**IsPoolGPUStreamThread**( )](../api/library/filesystem/class.asyncqueue_cs.md#isPoolGPUStreamThread_bool)* instead. |
| ***IsFileStreamThread**( )* | Renamed. Use *[**IsPoolFileStreamThread**( )](../api/library/filesystem/class.asyncqueue_cs.md#isPoolFileStreamThread_bool)* instead. |
| ***IsAsyncThread**( )* | Renamed. Use *[**IsPoolAsyncThread**( )](../api/library/filesystem/class.asyncqueue_cs.md#isPoolAsyncThread_bool)* instead. |
| ***IsBackgroundThread**( )* | Renamed. Use *[**IsPoolBackgroundThread**( )](../api/library/filesystem/class.asyncqueue_cs.md#isPoolBackgroundThread_bool)* instead. |
| ***IsAsyncRenderThread**( )* | Renamed. Use *[**IsPoolRenderFlushThread**( )](../api/library/filesystem/class.asyncqueue_cs.md#isPoolRenderFlushThread_bool)* instead. |
| ***IsPoolCPUShaderThread**( )* | Removed. |


#### New Functions


- *[ASYNC_THREAD.SYNC](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_THREAD_SYNC)*
- *[ASYNC_THREAD.COMMON](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_THREAD_COMMON)*
- *[ASYNC_THREAD.CRITICAL](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_THREAD_CRITICAL)*
- *[ASYNC_PRIORITY.HIGHEST](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_PRIORITY_HIGHEST)*
- *[ASYNC_PRIORITY.ABOVENORMAL](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_PRIORITY_ABOVENORMAL)*
- *[ASYNC_PRIORITY.NORMAL](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_PRIORITY_NORMAL)*
- *[ASYNC_PRIORITY.BELOWNORMAL](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_PRIORITY_BELOWNORMAL)*
- *[ASYNC_PRIORITY.LOWEST](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_PRIORITY_LOWEST)*
- *[ASYNC_PRIORITY.IDLE](../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_PRIORITY_IDLE)*
- *[**IsPoolSyncThread**( )](../api/library/filesystem/class.asyncqueue_cs.md#isPoolSyncThread_bool)*
- *[**IsPoolCommonThread**( )](../api/library/filesystem/class.asyncqueue_cs.md#isPoolCommonThread_bool)*
- *[**IsPoolCriticalThread**( )](../api/library/filesystem/class.asyncqueue_cs.md#isPoolCriticalThread_bool)*
- *[**IsPoolRenderFlushThread**( )](../api/library/filesystem/class.asyncqueue_cs.md#isPoolRenderFlushThread_bool)*


## Animations Class


#### New Functions


- *[**GetAnimScriptTypeName**( int )](../api/library/animations/class.animations_cs.md#getAnimScriptTypeName_int_cstr)*
- *[**RebuildAnimScripts**( )](../api/library/animations/class.animations_cs.md#rebuildAnimScripts_void)*


#### New Properties


- *[**IsAnimScriptsLoaded**](../api/library/animations/class.animations_cs.md#IsAnimScriptsLoaded)*
- *[**IsAnimScriptsRebuilding**](../api/library/animations/class.animations_cs.md#IsAnimScriptsRebuilding)*
- *[**IsAnimScriptsSuccessBuild**](../api/library/animations/class.animations_cs.md#IsAnimScriptsSuccessBuild)*
- *[**NumAnimScriptTypes**](../api/library/animations/class.animations_cs.md#NumAnimScriptTypes)*
- *[**EventCustomLibBuild**](../api/library/animations/class.animations_cs.md#EventCustomLibBuild)*


## CPUShader Class


#### New Functions


- *[PoolType.Auto](../api/library/common/mt/class.cpushader_cs.md#PoolType_Auto)*
- *[PoolType.Async](../api/library/common/mt/class.cpushader_cs.md#PoolType_Async)*
- *[PoolType.Sync](../api/library/common/mt/class.cpushader_cs.md#PoolType_Sync)*
- *[PoolType.Critical](../api/library/common/mt/class.cpushader_cs.md#PoolType_Critical)*
- *[PoolType.Background](../api/library/common/mt/class.cpushader_cs.md#PoolType_Background)*
- *[PoolType.RenderFlush](../api/library/common/mt/class.cpushader_cs.md#PoolType_RenderFlush)*
- *[PoolType.FileStream](../api/library/common/mt/class.cpushader_cs.md#PoolType_FileStream)*
- *[PoolType.GPUStream](../api/library/common/mt/class.cpushader_cs.md#PoolType_GPUStream)*


## EditorLogic Class


In previous SDK versions callbacks were only triggered for [non-hidden](../code/formats/property_format.md#property_hidden) properties, starting from 2.21 callbacks are triggered for *hidden* ones as well.


## Ffp Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***TEXTURE_SAMPLE_SHADOW*** | Removed. |


## FileSystem Class


#### New Functions


- *[**GetPackagesVirtualPaths**( string[] )](../api/library/filesystem/class.filesystem_cs.md#getPackagesVirtualPaths_VECString_void)*
- *[**IsPackageLoaded**( string )](../api/library/filesystem/class.filesystem_cs.md#isPackageLoaded_cstr_bool)*


## Gui Class


#### New Functions


- *[**GetFontFallback**( string, string[] )](../api/library/gui/class.gui_cs.md#getFontFallback_cstr_VECString_void)*
- *[**SetFontFallback**( string, string[] )](../api/library/gui/class.gui_cs.md#setFontFallback_cstr_VECString_void)*
- *[**GetGlobalFontFallback**( string[] )](../api/library/gui/class.gui_cs.md#getGlobalFontFallback_VECString_void)*
- *[**SetGlobalFontFallback**( string[] )](../api/library/gui/class.gui_cs.md#setGlobalFontFallback_VECString_void)*


## ImportAnimation Class


The *ImportAnimation* class now supports a *[Skeleton](../api/library/common/import/class.importskeleton_cs.md)* reference, linking imported animations with their skeleton data.


#### New Properties


- *[**Skeleton**](../api/library/common/import/class.importanimation_cs.md#setSkeleton_ImportSkeleton_void)*


## ImportMesh Class


The *ImportMesh* class has been simplified. Animation-related properties (*AnimationFilepath*, *HasAnimations*) have been moved to the new *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cs.md)* class. *ImportMesh* now represents only static mesh data.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| Property **AnimationFilepath** | Moved to *[**ImportMeshSkinned**](../api/library/common/import/class.importmeshskinned_cs.md)*. |
| Property **HasAnimations** | Removed. Use *[**ImportMeshSkinned**](../api/library/common/import/class.importmeshskinned_cs.md)* for skinned mesh data. |


## ImportNode Class


The *ImportNode* class now supports a *[MeshSkinned](../api/library/common/import/class.importmeshskinned_cs.md)* reference, separating skinned and static mesh data during import.


#### New Properties


- *[**MeshSkinned**](../api/library/common/import/class.importnode_cs.md#setMeshSkinned_ImportMeshSkinned_void)*


## ImportProcessor Class


The *ImportProcessor* class has been updated to support the new skeletal animation pipeline. Animation processing methods now use *[MeshSkinnedAnimation](../api/library/rendering/class.meshskinnedanimation_cs.md)* and *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cs.md)* instead of *MeshAnimation* and *ImportMesh*. New methods have been added for processing skinned meshes and skeletons.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***ProcessAnimation**( MeshAnimation, ImportAnimation )* | Signature changed: *[**ProcessAnimation**( MeshSkinnedAnimation, ImportAnimation )](../api/library/common/import/class.importprocessor_cs.md#processAnimation_MeshSkinnedAnimation_ImportAnimation_bool)*. |
| ***ProcessAnimation**( MeshAnimation, ImportMesh, ImportAnimation )* | Signature changed: *[**ProcessAnimation**( MeshSkinnedAnimation, ImportMeshSkinned, ImportAnimation )](../api/library/common/import/class.importprocessor_cs.md#processAnimation_MeshSkinnedAnimation_ImportMeshSkinned_ImportAnimation_bool)*. |
| ***OnProcessAnimation**( MeshAnimation, ImportAnimation )* | Signature changed: ***OnProcessAnimation**( MeshSkinnedAnimation, ImportAnimation )*. |
| ***OnProcessAnimation**( MeshAnimation, ImportMesh, ImportAnimation )* | Signature changed: ***OnProcessAnimation**( MeshSkinnedAnimation, ImportMeshSkinned, ImportAnimation )*. |


#### New Functions


- *[**ProcessMeshSkinned**( MeshSkinned, ImportMeshSkinned )](../api/library/common/import/class.importprocessor_cs.md#processMeshSkinned_MeshSkinned_ImportMeshSkinned_bool)*
- ***OnProcessMeshSkinned**( MeshSkinned, ImportMeshSkinned )*
- *[**ProcessSkeleton**( Skeleton, ImportSkeleton )](../api/library/common/import/class.importprocessor_cs.md#processSkeleton_Skeleton_ImportSkeleton_bool)*
- ***OnProcessSkeleton**( Skeleton, ImportSkeleton )*


## ImportScene Class


The *ImportScene* class now supports *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cs.md)* and *[ImportSkeleton](../api/library/common/import/class.importskeleton_cs.md)* objects as separate entities, enabling proper handling of skinned meshes and skeletons during import.


#### New Functions


- *[**GetNumMeshSkinneds**( )](../api/library/common/import/class.importscene_cs.md#getNumMeshSkinneds_int)*
- *[**GetMeshSkinned**( int )](../api/library/common/import/class.importscene_cs.md#getMeshSkinned_int_ImportMeshSkinned)*
- *[**AddMeshSkinned**( ImportNode )](../api/library/common/import/class.importscene_cs.md#addMeshSkinned_ImportNode_ImportMeshSkinned)*
- *[**RemoveMeshSkinned**( ImportMeshSkinned )](../api/library/common/import/class.importscene_cs.md#removeMeshSkinned_ImportMeshSkinned_void)*
- *[**GetNumSkeletons**( )](../api/library/common/import/class.importscene_cs.md#getNumSkeletons_int)*
- *[**GetSkeleton**( int )](../api/library/common/import/class.importscene_cs.md#getSkeleton_int_ImportSkeleton)*
- *[**AddSkeleton**( )](../api/library/common/import/class.importscene_cs.md#addSkeleton_ImportSkeleton)*
- *[**RemoveSkeleton**( ImportSkeleton )](../api/library/common/import/class.importscene_cs.md#removeSkeleton_ImportSkeleton_void)*


## Importer Class


The *Importer* class has been updated for the new skeletal animation pipeline. The *IMPORT_JOINTS* flag has been renamed as *IMPORT_SKELETONS*. Animation import methods now use *[MeshSkinnedAnimation](../api/library/rendering/class.meshskinnedanimation_cs.md)* and *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cs.md)* instead of *MeshAnimation* and *ImportMesh*. New methods and processors have been added for importing skinned meshes and skeletons.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***IMPORT_JOINTS*** | Renamed as *[**IMPORT_SKELETONS**](../api/library/common/import/class.importer_cs.md#IMPORT_SKELETONS)*. |
| ***ImportAnimation**( ImportProcessor, MeshAnimation, ImportAnimation )* | Signature changed: *[**ImportAnimation**( ImportProcessor, MeshSkinnedAnimation, ImportAnimation )](../api/library/common/import/class.importer_cs.md#importAnimation_ImportProcessor_MeshSkinnedAnimation_ImportAnimation_bool)*. |
| ***ImportAnimation**( ImportProcessor, MeshAnimation, ImportMesh, ImportAnimation )* | Signature changed: *[**ImportAnimation**( ImportProcessor, MeshSkinnedAnimation, ImportMeshSkinned, ImportAnimation )](../api/library/common/import/class.importer_cs.md#importAnimation_ImportProcessor_MeshSkinnedAnimation_ImportMeshSkinned_ImportAnimation_bool)*. |
| ***OnImportAnimation**( ImportProcessor, MeshAnimation, ImportAnimation )* | Signature changed: ***OnImportAnimation**( ImportProcessor, MeshSkinnedAnimation, ImportAnimation )*. |
| ***OnImportAnimation**( ImportProcessor, MeshAnimation, ImportMesh, ImportAnimation )* | Signature changed: ***OnImportAnimation**( ImportProcessor, MeshSkinnedAnimation, ImportMeshSkinned, ImportAnimation )*. |
| ***CheckSupportedAnimation**( ImportMesh, ImportAnimation )* | Signature changed: *[**CheckSupportedAnimation**( ImportMeshSkinned, ImportAnimation )](../api/library/common/import/class.importer_cs.md#checkSupportedAnimation_ImportMeshSkinned_ImportAnimation_bool)*. |
| ***CheckDefaultAnimation**( ImportMesh, ImportAnimation )* | Signature changed: *[**CheckDefaultAnimation**( ImportMeshSkinned, ImportAnimation )](../api/library/common/import/class.importer_cs.md#checkDefaultAnimation_ImportMeshSkinned_ImportAnimation_bool)*. |
| ***OnCheckSupportedAnimation**( ImportMesh, ImportAnimation )* | Signature changed: ***OnCheckSupportedAnimation**( ImportMeshSkinned, ImportAnimation )*. |
| ***OnCheckDefaultAnimation**( ImportMesh, ImportAnimation )* | Signature changed: ***OnCheckDefaultAnimation**( ImportMeshSkinned, ImportAnimation )*. |


#### New Properties


- *[**MeshSkinnedsProcessor**](../api/library/common/import/class.importer_cs.md#setMeshSkinnedsProcessor_cstr_void)*
- *[**SkeletonsProcessor**](../api/library/common/import/class.importer_cs.md#setSkeletonsProcessor_cstr_void)*


#### New Functions


- *[**ImportMeshSkinned**( ImportProcessor, MeshSkinned, ImportMeshSkinned )](../api/library/common/import/class.importer_cs.md#importMeshSkinned_ImportProcessor_MeshSkinned_ImportMeshSkinned_bool)*
- *[**ImportSkeleton**( ImportProcessor, Skeleton, ImportSkeleton )](../api/library/common/import/class.importer_cs.md#importSkeleton_ImportProcessor_Skeleton_ImportSkeleton_bool)*
- ***OnImportMeshSkinned**( ImportProcessor, MeshSkinned, ImportMeshSkinned )*
- ***OnImportSkeleton**( ImportProcessor, Skeleton, ImportSkeleton )*


## Material Class


#### New Functions


- *[TEXTURE_SOURCE_REFLECTION_SKY](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_REFLECTION_SKY)*
- *[TEXTURE_SOURCE_REFLECTION_VOXEL_PROBE](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_REFLECTION_VOXEL_PROBE)*
- *[TEXTURE_SOURCE_REFLECTION_ENV_PROBE](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_REFLECTION_ENV_PROBE)*


## Mesh Class


All bone-related methods have been removed - skeleton data is now managed via the *[Skeleton](../api/library/animations/skeletal/class.skeleton_cs.md)* class. All morph target-related methods (*SurfaceTarget*, *Weight*) have been removed. The *target* parameter has been removed from vertex, normal, tangent, intersection, and surface methods.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| Property **NumBones** | Removed. |
| ***SetBoneName**( int, string )* | Removed. |
| ***GetBoneName**( int )* | Removed. |
| ***SetBoneParent**( int, int )* | Removed. |
| ***GetBoneParent**( int )* | Removed. |
| ***SetBoneTransform**( int, mat4 )* | Removed. |
| ***GetBoneTransform**( int )* | Removed. |
| ***SetBoneTransforms**( mat4[] )* | Removed. |
| ***GetBoneTransforms**( mat4[] )* | Removed. |
| ***GetNumBones**( )* | Removed. |
| ***SetNumSurfaceTargets**( int, int )* | Removed. |
| ***GetNumSurfaceTargets**( int )* | Removed. |
| ***SetNumWeights**( int, int )* | Removed. |
| ***GetNumWeights**( int )* | Removed. |
| ***SetSurfaceTargetName**( int, int, string )* | Removed. |
| ***GetSurfaceTargetName**( int, int )* | Removed. |
| *[**GetIntersection**( dvec3, dvec3, dvec3[], vec3[], int[], int )](../api/library/rendering/class.mesh_cs.md#getIntersection_dvec3_dvec3_dvec3_vec3_int_int_int)* | Set of arguments changed. |
| ***SetWeightBones**( int, ivec4, int )* | Removed. |
| ***GetWeightBones**( int, int )* | Removed. |
| ***SetWeightCount**( int, int, int )* | Removed. |
| ***GetWeightCount**( int, int )* | Removed. |
| ***SetWeightWeights**( int, vec4, int )* | Removed. |
| ***GetWeightWeights**( int, int )* | Removed. |
| ***AddBone**( string, int )* | Removed. |
| ***AddSurfaceTarget**( int, string )* | Removed. |
| ***FindBone**( string )* | Removed. |
| ***FindSurfaceTarget**( int, string )* | Removed. |
| *[**GetIntersection**( vec3, vec3, vec3[], vec3[], int[], int )](../api/library/rendering/class.mesh_cs.md#getIntersection_vec3_vec3_vec3_vec3_int_int_int)* | Set of arguments changed. |
| *[**SetNormal**( int, vec3, int )](../api/library/rendering/class.mesh_cs.md#setNormal_int_vec3_int_void)* | Set of arguments changed. |
| *[**GetNormal**( int, int )](../api/library/rendering/class.mesh_cs.md#getNormal_int_int_vec3)* | Set of arguments changed. |
| *[**SetNumNormals**( int, int )](../api/library/rendering/class.mesh_cs.md#setNumNormals_int_int_void)* | Set of arguments changed. |
| *[**GetNumNormals**( int )](../api/library/rendering/class.mesh_cs.md#getNumNormals_int_int)* | Set of arguments changed. |
| *[**SetNumTangents**( int, int )](../api/library/rendering/class.mesh_cs.md#setNumTangents_int_int_void)* | Set of arguments changed. |
| *[**GetNumTangents**( int )](../api/library/rendering/class.mesh_cs.md#getNumTangents_int_int)* | Set of arguments changed. |
| *[**SetNumVertex**( int, int )](../api/library/rendering/class.mesh_cs.md#setNumVertex_int_int_void)* | Set of arguments changed. |
| *[**GetNumVertex**( int )](../api/library/rendering/class.mesh_cs.md#getNumVertex_int_int)* | Set of arguments changed. |
| *[**SetSurfaceTransform**( mat4, int )](../api/library/rendering/class.mesh_cs.md#setSurfaceTransform_mat4_int_int)* | Set of arguments changed. |
| *[**SetTangent**( int, quat, int )](../api/library/rendering/class.mesh_cs.md#setTangent_int_quat_int_void)* | Set of arguments changed. |
| *[**GetTangent**( int, int )](../api/library/rendering/class.mesh_cs.md#getTangent_int_int_quat)* | Set of arguments changed. |
| *[**SetVertex**( int, vec3, int )](../api/library/rendering/class.mesh_cs.md#setVertex_int_vec3_int_void)* | Set of arguments changed. |
| *[**GetVertex**( int, int )](../api/library/rendering/class.mesh_cs.md#getVertex_int_int_vec3)* | Set of arguments changed. |
| *[**AddMeshSurface**( int, Mesh, int, int )](../api/library/rendering/class.mesh_cs.md#addMeshSurface_int_ConstMesh_int_int_int)* | Set of arguments changed. |
| *[**AddMeshSurface**( string, Mesh, int, int )](../api/library/rendering/class.mesh_cs.md#addMeshSurface_cstr_ConstMesh_int_int_int)* | Set of arguments changed. |
| *[**AddNormal**( vec3, int )](../api/library/rendering/class.mesh_cs.md#addNormal_vec3_int_void)* | Set of arguments changed. |
| *[**AddTangent**( quat, int )](../api/library/rendering/class.mesh_cs.md#addTangent_quat_int_void)* | Set of arguments changed. |
| *[**AddVertex**( vec3, int )](../api/library/rendering/class.mesh_cs.md#addVertex_vec3_int_void)* | Set of arguments changed. |
| *[**AddVertex**( vec3[], int )](../api/library/rendering/class.mesh_cs.md#addVertex_VECvec3_int_void)* | Set of arguments changed. |
| *[**CreateNormals**( int )](../api/library/rendering/class.mesh_cs.md#createNormals_int_int)* | Set of arguments changed. |
| *[**CreateNormals**( float, int )](../api/library/rendering/class.mesh_cs.md#createNormals_float_int_int)* | Set of arguments changed. |
| *[**CreateTangents**( int )](../api/library/rendering/class.mesh_cs.md#createTangents_int_int)* | Set of arguments changed. |
| *[**AddNormals**( vec3[], int )](../api/library/rendering/class.mesh_cs.md#addNormals_VECvec3_int_void)* | Set of arguments changed. |
| *[**AddTangents**( quat[], int )](../api/library/rendering/class.mesh_cs.md#addTangents_VECquat_int_void)* | Set of arguments changed. |
| *[**GetVertices**( int )](../api/library/rendering/class.mesh_cs.md#getVertices_int_VECvec3)* | Set of arguments changed. |
| *[**GetNormals**( int )](../api/library/rendering/class.mesh_cs.md#getNormals_int_VECvec3)* | Set of arguments changed. |
| *[**GetTangents**( int )](../api/library/rendering/class.mesh_cs.md#getTangents_int_VECquat)* | Set of arguments changed. |
| *[**ClearSurface**( int )](../api/library/rendering/class.mesh_cs.md#clearSurface_int_void)* | Set of arguments changed. |


## MeshAnimation Class


The *MeshAnimation* class has been renamed as *[MeshSkinnedAnimation](../api/library/rendering/class.meshskinnedanimation_cs.md)*. The API has been reworked: bone-based methods have been replaced with joint-based methods, and the class now references a shared *[Skeleton](../api/library/animations/skeletal/class.skeleton_cs.md)*.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| Class **MeshAnimation** | Renamed as *[**MeshSkinnedAnimation**](../api/library/rendering/class.meshskinnedanimation_cs.md)*. |
| Property **NumBones** | Replaced with *[**NumSrcJoints**](../api/library/rendering/class.meshskinnedanimation_cs.md#getNumSrcJoints_int)*. |
| ***FindBone**( string )* | Replaced with *[**FindSrcJoint**( string )](../api/library/rendering/class.meshskinnedanimation_cs.md#findSrcJoint_cstr_int)*. |
| ***AddBone**( string, int )* | Removed. Skeleton data is now managed via *[Skeleton](../api/library/animations/skeletal/class.skeleton_cs.md)*. |
| ***SetBoneName**( int, string )* | Removed. Use *[**GetSrcJointName**( int )](../api/library/rendering/class.meshskinnedanimation_cs.md#getSrcJointName_int_cstr)* (read-only). |
| ***GetBoneName**( int )* | Replaced with *[**GetSrcJointName**( int )](../api/library/rendering/class.meshskinnedanimation_cs.md#getSrcJointName_int_cstr)*. |
| ***SetBoneParent**( int, int )* | Removed. Use *[**GetSrcJointParent**( int )](../api/library/rendering/class.meshskinnedanimation_cs.md#getSrcJointParent_int_int)* (read-only). |
| ***GetBoneParent**( int )* | Replaced with *[**GetSrcJointParent**( int )](../api/library/rendering/class.meshskinnedanimation_cs.md#getSrcJointParent_int_int)*. |
| ***SetBoneTransform**( int, mat4 )* | Removed. Use frame-based methods. |
| ***GetBoneTransform**( int )* | Removed. Use frame-based methods. |
| Property **NumAnimationBones** | Replaced with *[**NumAnimatedJoints**](../api/library/rendering/class.meshskinnedanimation_cs.md#getNumAnimatedJoints_int)*. |


## Node Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***TYPE.WORLD_TRANSFORM_BONE*** | Renamed as *[**TYPE.WORLD_TRANSFORM_JOINT**](../api/library/nodes/class.node_cs.md#WORLD_TRANSFORM_JOINT)*. |


#### New Functions


- *[TYPE.NODE_SKELETON_POSE](../api/library/nodes/class.node_cs.md#NODE_SKELETON_POSE)*
- *[TYPE.OBJECT_MESH_SKINNED_LEGACY](../api/library/nodes/class.node_cs.md#OBJECT_MESH_SKINNED_LEGACY)*


## ObjectMeshSkinned Class


The *ObjectMeshSkinned* class has been completely reworked. The previous class (with animation layers, bone transforms, IK chains, look-at chains, constraints, retargeting, and animation playback) has been renamed as *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. A new simplified *[ObjectMeshSkinned](../api/library/objects/class.objectmeshskinned_cs.md)* class has been created, which provides only mesh data access, joint transforms, and morph targets. If your code uses any of the removed functionality, switch to *ObjectMeshSkinnedLegacy*.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***GetMesh**( Mesh )* | Set of arguments changed: *[**GetMesh**( MeshSkinned )](../api/library/objects/class.objectmeshskinned_cs.md#getMesh_MeshSkinned_int)*. |
| ***ApplyMeshProcedural**( Mesh )* | Set of arguments changed: *[**ApplyMeshProcedural**( MeshSkinned )](../api/library/objects/class.objectmeshskinned_cs.md#applyMeshProcedural_ConstMeshSkinned_int)*. |
| All animation playback methods (**Play**, **Stop**, **IsPlaying**, **IsStopped**, properties **Controlled**, **Loop**, **Time**, **Speed**, **AnimPath**, **InterpolationAccuracy**) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All layer methods (**AddLayer**, **RemoveLayer**, **SetLayerEnabled**, **SetLayerWeight**, **CopyLayer**, **LerpLayer**, **MulLayer**, **SetLayerBoneTransform**, **SetLayerFrame**, **SetLayerAnimationFilePath**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All bone methods (**GetNumBones**, **GetBoneName**, **FindBone**, **GetBoneParent**, **SetBoneTransform**, **GetBoneSkinningTransform**, **GetBoneBindLocalTransform**, **CopyBoneTransforms**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All retargeting methods (**SetRetargeting**, **RemoveRetargeting**, **GetRetargeting**, **IsRetargeting**) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All IK chain methods (**AddIKChain**, **SetIKChainEnabled**, **SetIKChainTargetPosition**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All look-at chain methods (**AddLookAtChain**, **SetLookAtChainEnabled**, **SetLookAtChainTargetPosition**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All bone constraint methods (**AddBoneConstraint**, **SetBoneConstraintEnabled**, **SetBoneConstraintYawAngles**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All bind node methods (**SetBindNode**, **GetBindNode**, **SetBindNodeSpace**, **SetBindMode**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All visualization methods (**SetVisualizeAllBones**, **AddVisualizeBone**, **AddVisualizeIKChain**, **AddVisualizeLookAtChain**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All events (**EventUpdate**, **EventBeginLookAtSolvers**, **EventEndLookAtSolvers**, **EventBeginIKSolvers**, **EventEndIKSolvers**, **EventBeginBoneConstraints**, **EventEndBoneConstraints**) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |
| All enums (**BIND_MODE**, **NODE_SPACE**, **BONE_SPACE**, **ANIM_FRAME_USES**, **INTERPOLATION_ACCURACY**, **CHAIN_CONSTRAINT**) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cs.md)*. |


#### New Functions


- *[**GetNumJoints**( )](../api/library/objects/class.objectmeshskinned_cs.md#getNumJoints_int)*
- *[**GetJointRestLocalTransform**( int )](../api/library/objects/class.objectmeshskinned_cs.md#getJointRestLocalTransform_int_mat4)*
- *[**GetJointSkinningTransform**( int )](../api/library/objects/class.objectmeshskinned_cs.md#getJointSkinningTransform_int_mat4)*
- *[**GetSurfaceName**( int )](../api/library/objects/class.objectmeshskinned_cs.md#getSurfaceName_int_cstr)*
- *[**FindSurface**( string )](../api/library/objects/class.objectmeshskinned_cs.md#findSurface_cstr_int)*


#### New Properties


- *[**NumJoints**](../api/library/objects/class.objectmeshskinned_cs.md#NumJoints)*


## Profiler Class


#### New Functions


- *[**StartProfilerDump**( float, string )](../api/library/engine/class.profiler_cs.md#startProfilerDump_float_cstr_void)*
- *[**StartProfilerDump**( int, string )](../api/library/engine/class.profiler_cs.md#startProfilerDump_int_cstr_void)*
- *[**StartProfilerDump**( string )](../api/library/engine/class.profiler_cs.md#startProfilerDump_cstr_void)*
- *[**StopProfilerDump**( )](../api/library/engine/class.profiler_cs.md#stopProfilerDump_void)*
- *[**IsProfilerDumpEnabled**( )](../api/library/engine/class.profiler_cs.md#isProfilerDumpEnabled_int)*


#### New Properties


- *[**EventProfileDumpStart**](../api/library/engine/class.profiler_cs.md#EventProfileDumpStart)*
- *[**EventProfileDumpEnd**](../api/library/engine/class.profiler_cs.md#EventProfileDumpEnd)*


## Properties Class


#### New Properties


- *[**ValidationEnabled**](../api/library/engine/class.properties_cs.md#ValidationEnabled)*


## Render Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| *[**MemoryClear**( bool )](../api/library/rendering/class.render_cs.md#memoryClear_int_void)* | Set of arguments changed. |
| Property **TransparentMultipleEnvProbes** | Removed. |
| Property **TransparentLight** | Removed. |
| Property **TransparentAmbient** | Removed. |
| Property **LightsTileGridSize** | Removed. |
| Property **LightsMaxPerBatch** | Removed. |
| Property **SSSSSTAAMaxFramesByVelocity** | Removed. |
| Property **SSSSSTAAMinFramesByVelocity** | Removed. |
| Property **TAAMaxFramesByVelocity** | Removed. |
| Property **TAAMinFramesByVelocity** | Removed. |
| Property **TAAInformationLostFrameCount** | Removed. |
| Property **FSRAutoReactiveEnabled** | Removed. |
| Property **FSRAutoReactiveScale** | Removed. |
| Property **FSRAutoTCScale** | Removed. |
| Property **FSRAutoTCThreshold** | Removed. |
| Property **FSRAutoReactiveMax** | Removed. |
| Property **FSRAutoReactiveMax** | Removed. |
| Property **UpscalePost** | Removed. |


#### New Functions


- *[RENDER_FSR_MODE.NATIVE_AA](../api/library/rendering/class.render_cs.md#RENDER_FSR_MODE_NATIVE_AA)*
- *[RENDER_FSR_MODE.CUSTOM](../api/library/rendering/class.render_cs.md#RENDER_FSR_MODE_CUSTOM)*
- *[SHOW_VERTEX_DENSITY_MODE.DISCRETE_THRESHOLD](../api/library/rendering/class.render_cs.md#SHOW_VERTEX_DENSITY_MODE_DISCRETE_THRESHOLD)*
- *[SHOW_VERTEX_DENSITY_MODE.GRADIENT](../api/library/rendering/class.render_cs.md#SHOW_VERTEX_DENSITY_MODE_GRADIENT)*
- *[SHOW_QUAD_OVERDRAW_DISPLAY_MODE.GRADIENT](../api/library/rendering/class.render_cs.md#SHOW_QUAD_OVERDRAW_DISPLAY_MODE_GRADIENT)*
- *[SHOW_QUAD_OVERDRAW_DISPLAY_MODE.DISCRETE_THRESHOLD](../api/library/rendering/class.render_cs.md#SHOW_QUAD_OVERDRAW_DISPLAY_MODE_DISCRETE_THRESHOLD)*
- *[SHOW_QUAD_OVERDRAW_PASSES.ALL](../api/library/rendering/class.render_cs.md#SHOW_QUAD_OVERDRAW_PASSES_ALL)*
- *[SHOW_QUAD_OVERDRAW_PASSES.GEOMETRY](../api/library/rendering/class.render_cs.md#SHOW_QUAD_OVERDRAW_PASSES_GEOMETRY)*
- *[SHOW_QUAD_OVERDRAW_PASSES.GEOMETRY_WITHOUT_DEPTH_PRE_PASS](../api/library/rendering/class.render_cs.md#SHOW_QUAD_OVERDRAW_PASSES_GEOMETRY_WITHOUT_DEPTH_PRE_PASS)*
- *[PASS.VISUALIZER_QUAD_OVERDRAW](../api/library/rendering/class.render_cs.md#PASS_VISUALIZER_QUAD_OVERDRAW)*
- *[PASS.VISUALIZER_QUAD_OVERDRAW_NO_DEPTH_PREPASS](../api/library/rendering/class.render_cs.md#PASS_VISUALIZER_QUAD_OVERDRAW_NO_DEPTH_PREPASS)*
- *[SHADING_QUALITY.LOW](../api/library/rendering/class.render_cs.md#SHADING_QUALITY_LOW)*
- *[SHADING_QUALITY.MEDIUM](../api/library/rendering/class.render_cs.md#SHADING_QUALITY_MEDIUM)*
- *[SHADING_QUALITY.HIGH](../api/library/rendering/class.render_cs.md#SHADING_QUALITY_HIGH)*
- *[STREAMING_IGPU_VRAM_MODE.SYSTEM](../api/library/rendering/class.render_cs.md#STREAMING_IGPU_VRAM_MODE_SYSTEM)*
- *[STREAMING_IGPU_VRAM_MODE.SIZE](../api/library/rendering/class.render_cs.md#STREAMING_IGPU_VRAM_MODE_SIZE)*
- *[STREAMING_IGPU_VRAM_MODE.BALANCE](../api/library/rendering/class.render_cs.md#STREAMING_IGPU_VRAM_MODE_BALANCE)*
- *[RENDER_UPSCALE_ORDER.BEFORE_POST_EFFECTS](../api/library/rendering/class.render_cs.md#RENDER_UPSCALE_ORDER_BEFORE_POST_EFFECTS)*
- *[RENDER_UPSCALE_ORDER.AFTER_ADAPTATION_COLOR](../api/library/rendering/class.render_cs.md#RENDER_UPSCALE_ORDER_AFTER_ADAPTATION_COLOR)*
- *[RENDER_UPSCALE_ORDER.BEFORE_TAA](../api/library/rendering/class.render_cs.md#RENDER_UPSCALE_ORDER_BEFORE_TAA)*
- *[RENDER_UPSCALE_ORDER.AFTER_POST_EFFECTS](../api/library/rendering/class.render_cs.md#RENDER_UPSCALE_ORDER_AFTER_POST_EFFECTS)*
- *[RENDER_UPSCALE_ORDER.RENDER_UPSCALE_ORDER.AFTER_POST_EFFECTS](../api/library/rendering/class.render_cs.md#RENDER_UPSCALE_NUM_ORDERS)*


#### New Properties


- *[**EventBeginVisualizerQuadOverdraw**](../api/library/rendering/class.render_cs.md#EventBeginVisualizerQuadOverdraw)*
- *[**EventEndVisualizerQuadOverdraw**](../api/library/rendering/class.render_cs.md#EventEndVisualizerQuadOverdraw)*
- *[**EventGPUCrashDump**](../api/library/rendering/class.render_cs.md#EventGPUCrashDump)*
- *[**OccluderDistance**](../api/library/rendering/class.render_cs.md#OccluderDistance)*
- *[**UpscaleFixFlicker**](../api/library/rendering/class.render_cs.md#UpscaleFixFlicker)*
- *[**DLSSResolutionScaleValue**](../api/library/rendering/class.render_cs.md#DLSSResolutionScaleValue)*
- *[**DLSSResolutionScaleEnabled**](../api/library/rendering/class.render_cs.md#DLSSResolutionScaleEnabled)*
- *[**FSRCustomResolutionScale**](../api/library/rendering/class.render_cs.md#FSRCustomResolutionScale)*
- *[**CloudsEnvironmentTexturePath**](../api/library/rendering/class.render_cs.md#CloudsEnvironmentTexturePath)*
- *[**CloudsEnvironmentSky**](../api/library/rendering/class.render_cs.md#CloudsEnvironmentSky)*
- *[**CloudsEnvironmentSkyColor**](../api/library/rendering/class.render_cs.md#CloudsEnvironmentSkyColor)*
- *[**CloudsEnvironmentColor**](../api/library/rendering/class.render_cs.md#CloudsEnvironmentColor)*
- *[**SharpenResolution**](../api/library/rendering/class.render_cs.md#SharpenResolution)*
- *[**ShowProjAndOmniShadowCasters**](../api/library/rendering/class.render_cs.md#ShowProjAndOmniShadowCasters)*
- *[**ShowDepthPrePass**](../api/library/rendering/class.render_cs.md#ShowDepthPrePass)*
- *[**ShowTransparentGBuffer**](../api/library/rendering/class.render_cs.md#ShowTransparentGBuffer)*
- *[**ShowTransparentLightingAmbient**](../api/library/rendering/class.render_cs.md#ShowTransparentLightingAmbient)*
- *[**ShowTransparentLightingEnvironmentProbe**](../api/library/rendering/class.render_cs.md#ShowTransparentLightingEnvironmentProbe)*
- *[**ShowTransparentLightingVoxelProbe**](../api/library/rendering/class.render_cs.md#ShowTransparentLightingVoxelProbe)*
- *[**ShowTransparentLightingPlanarProbe**](../api/library/rendering/class.render_cs.md#ShowTransparentLightingPlanarProbe)*
- *[**ShowTransparentLightingLightOmni**](../api/library/rendering/class.render_cs.md#ShowTransparentLightingLightOmni)*
- *[**ShowTransparentLightingLightProj**](../api/library/rendering/class.render_cs.md#ShowTransparentLightingLightProj)*
- *[**ShowTransparentLightingLightWorld**](../api/library/rendering/class.render_cs.md#ShowTransparentLightingLightWorld)*
- *[**ShowVertexDensityEnabled**](../api/library/rendering/class.render_cs.md#ShowVertexDensityEnabled)*
- *[**ShowVertexDensityMode**](../api/library/rendering/class.render_cs.md#ShowVertexDensityMode)*
- *[**ShowVertexDensityDepthTest**](../api/library/rendering/class.render_cs.md#ShowVertexDensityDepthTest)*
- *[**ShowVertexDensitySearchArea**](../api/library/rendering/class.render_cs.md#ShowVertexDensitySearchArea)*
- *[**ShowVertexDensityThreshold**](../api/library/rendering/class.render_cs.md#ShowVertexDensityThreshold)*
- *[**ShowVertexDensityBlend**](../api/library/rendering/class.render_cs.md#ShowVertexDensityBlend)*
- *[**ShowQuadOverdrawEnabled**](../api/library/rendering/class.render_cs.md#ShowQuadOverdrawEnabled)*
- *[**ShowQuadOverdrawDisplayMode**](../api/library/rendering/class.render_cs.md#ShowQuadOverdrawDisplayMode)*
- *[**ShowQuadOverdrawPasses**](../api/library/rendering/class.render_cs.md#ShowQuadOverdrawPasses)*
- *[**ShowQuadOverdrawWireframe**](../api/library/rendering/class.render_cs.md#ShowQuadOverdrawWireframe)*
- *[**ShowQuadOverdrawLandscapeTerrain**](../api/library/rendering/class.render_cs.md#ShowQuadOverdrawLandscapeTerrain)*
- *[**ShowQuadOverdrawWaterGlobal**](../api/library/rendering/class.render_cs.md#ShowQuadOverdrawWaterGlobal)*
- *[**ShowQuadOverdrawThreshold**](../api/library/rendering/class.render_cs.md#ShowQuadOverdrawThreshold)*
- *[**ShowQuadOverdrawBlend**](../api/library/rendering/class.render_cs.md#ShowQuadOverdrawBlend)*
- *[**EnvironmentHazeResolution**](../api/library/rendering/class.render_cs.md#EnvironmentHazeResolution)*
- *[**ShadingQuality**](../api/library/rendering/class.render_cs.md#ShadingQuality)*
- *[**NumCompiledPSOGlobal**](../api/library/rendering/class.render_cs.md#NumCompiledPSOGlobal)*
- *[**StreamingIGpuVRAMMode**](../api/library/rendering/class.render_cs.md#StreamingIGpuVRAMMode)*
- *[**StreamingIGpuVRAMSize**](../api/library/rendering/class.render_cs.md#StreamingIGpuVRAMSize)*
- *[**StreamingIGpuVRAMBalance**](../api/library/rendering/class.render_cs.md#StreamingIGpuVRAMBalance)*
- *[**UpscaleOrder**](../api/library/rendering/class.render_cs.md#UpscaleOrder)*
- *[**FSRShowDebugView**](../api/library/rendering/class.render_cs.md#FSRShowDebugView)*
- *[**EnvironmentDitherScale**](../api/library/rendering/class.render_cs.md#EnvironmentDitherScale)*
- *[**EnvironmentHazeDitherScale**](../api/library/rendering/class.render_cs.md#EnvironmentHazeDitherScale)*
- *[**EnvironmentSunAngularSize**](../api/library/rendering/class.render_cs.md#EnvironmentSunAngularSize)*
- *[**EnvironmentMoonAngularSize**](../api/library/rendering/class.render_cs.md#EnvironmentMoonAngularSize)*
- *[**LightsDitherScale**](../api/library/rendering/class.render_cs.md#LightsDitherScale)*
- *[**StreamingFreeSpaceRAMCommitted**](../api/library/rendering/class.render_cs.md#StreamingFreeSpaceRAMCommitted)*


## Renderer Class


#### New Functions


- *[**UseDepthPrePass**( )](../api/library/rendering/class.renderer_cs.md#useDepthPrePass_int)*


## RenderState Class


#### New Functions


- *[RENDER_MODE.POINTS](../api/library/rendering/class.renderstate_cs.md#RENDER_MODE_POINTS)*
- *[RENDER_MODE.LINES](../api/library/rendering/class.renderstate_cs.md#RENDER_MODE_LINES)*
- *[RENDER_MODE.TRIANGLES](../api/library/rendering/class.renderstate_cs.md#RENDER_MODE_TRIANGLES)*
- *[RENDER_MODE.TRIANGLE_PATCHES](../api/library/rendering/class.renderstate_cs.md#RENDER_MODE_TRIANGLE_PATCHES)*
- *[RENDER_MODE.QUAD_PATCHES](../api/library/rendering/class.renderstate_cs.md#RENDER_MODE_QUAD_PATCHES)*
- *[RENDER_MODE.NUM_RENDER_MODES](../api/library/rendering/class.renderstate_cs.md#NUM_RENDER_MODES)*
- *[**GetStructuredBuffer**( int )](../api/library/rendering/class.renderstate_cs.md#getStructuredBuffer_int_StructuredBuffer)*
- *[**SetIndexBuffer**( StructuredBuffer, int, int )](../api/library/rendering/class.renderstate_cs.md#setIndexBuffer_StructuredBuffer_int_int_void)*
- *[**SetVertexBuffer**( int, StructuredBuffer, int, int )](../api/library/rendering/class.renderstate_cs.md#setVertexBuffer_int_StructuredBuffer_int_int_void)*
- *[**Render**( RenderState.RENDER_MODE, int, int, int, int )](../api/library/rendering/class.renderstate_cs.md#render_int_int_int_int_int_int)*


#### New Properties


- *[**ConservativeRasterizationEnabled**](../api/library/rendering/class.renderstate_cs.md#ConservativeRasterizationEnabled)*
- *[**DepthWrite**](../api/library/rendering/class.renderstate_cs.md#DepthWrite)*


## Syncker::Manager Class


#### New Functions


- *[SPIDER_VISION_EASYBLEND_SYNC_TYPE.NETWORK](../api/library/plugins/syncker/class.syncker_manager_cs.md#NETWORK)*
- *[SPIDER_VISION_EASYBLEND_SYNC_TYPE.LOAD_FROM_LOCAL_STORAGE](../api/library/plugins/syncker/class.syncker_manager_cs.md#LOAD_FROM_LOCAL_STORAGE)*


#### New Properties


- *[**EasyblendSyncType**](../api/library/plugins/syncker/class.syncker_manager_cs.md#EasyblendSyncType)*


## SystemInfo Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***GetMemoryFree**( )* | Renamed as *[**GetRamFree**( )](../api/library/engine/class.systeminfo_cs.md#getRamFree_llong)*. |
| ***GetMemoryFreeCommitted**( )* | Renamed as *[**GetRamCommittedFree**( )](../api/library/engine/class.systeminfo_cs.md#getRamCommittedFree_llong)*. |
| ***GetMemoryTotal**( )* | Renamed as *[**GetRamTotal**( )](../api/library/engine/class.systeminfo_cs.md#getRamTotal_llong)*. |
| ***GetMemoryTotalCommitted**( )* | Renamed as *[**GetRamCommittedTotal**( )](../api/library/engine/class.systeminfo_cs.md#getRamCommittedTotal_llong)*. |
| ***GetMemoryUsage**( )* | Renamed as *[**GetRamUsage**( )](../api/library/engine/class.systeminfo_cs.md#getRamUsage_llong)*. |
| ***GetMemoryUsageCommitted**( )* | Renamed as *[**GetRamCommittedUsage**( )](../api/library/engine/class.systeminfo_cs.md#getRamCommittedUsage_llong)*. |
| ***GetGPUMemoryFree**( )* | Renamed as *[**GetGpuVRamFree**( )](../api/library/engine/class.systeminfo_cs.md#getGpuVRamFree_llong)*. |
| ***GetGPUMemoryLimit**( )* | Renamed as *[**GetGpuVRamLimit**( )](../api/library/engine/class.systeminfo_cs.md#getGpuVRamLimit_llong)*. |
| ***GetGPUMemoryStatistics**( )* | Removed. Use *[**GetMemoryStatistics**( )](../api/library/engine/class.systeminfo_cs.md#getMemoryStatistics_MemoryStatistics)* instead. |


#### New Functions


- *[**GetGpuVRamTotal**( )](../api/library/engine/class.systeminfo_cs.md#getGpuVRamTotal_llong)*
- *[**GetGpuVRamBudget**( )](../api/library/engine/class.systeminfo_cs.md#getGpuVRamBudget_llong)*
- *[**GetGpuVRamLimit**( )](../api/library/engine/class.systeminfo_cs.md#getGpuVRamLimit_llong)*
- *[**GetGpuVRamBackground**( )](../api/library/engine/class.systeminfo_cs.md#getGpuVRamBackground_llong)*
- *[**GetGpuVRamUsage**( )](../api/library/engine/class.systeminfo_cs.md#getGpuVRamUsage_llong)*
- *[**GetGpuRamBackground**( )](../api/library/engine/class.systeminfo_cs.md#getGpuRamBackground_llong)*
- *[**GetGpuRamUsage**( )](../api/library/engine/class.systeminfo_cs.md#getGpuRamUsage_llong)*
- *[**GetRamCommittedLimit**( )](../api/library/engine/class.systeminfo_cs.md#getRamCommittedLimit_llong)*
- *[**GetRamCommittedBackground**( )](../api/library/engine/class.systeminfo_cs.md#getRamCommittedBackground_llong)*
- *[**GetRamLimit**( )](../api/library/engine/class.systeminfo_cs.md#getRamLimit_llong)*
- *[**OutOfVRam**( )](../api/library/engine/class.systeminfo_cs.md#outOfVRam_bool)*
- *[**OutOfRam**( )](../api/library/engine/class.systeminfo_cs.md#outOfRam_bool)*
- *[**OutOfRamCommitted**( )](../api/library/engine/class.systeminfo_cs.md#outOfRamCommitted_bool)*
- *[**GetMemoryStatistics**( )](../api/library/engine/class.systeminfo_cs.md#getMemoryStatistics_MemoryStatistics)*
- *[**GetRamFrequency**( )](../api/library/engine/class.systeminfo_cs.md#getRamFrequency_uint)*
- *[**GetSwapSize**( )](../api/library/engine/class.systeminfo_cs.md#getSwapSize_llong)*
- *[**GetCPUName**( )](../api/library/engine/class.systeminfo_cs.md#getCPUName_cstr)*
- *[**GetGPUUuidString**( int )](../api/library/engine/class.systeminfo_cs.md#getGPUUuidString_int_cstr)*
- *[**GetProcessID**( )](../api/library/engine/class.systeminfo_cs.md#getProcessID_int)*
- *[**GetEnvironmentVariable**( string )](../api/library/engine/class.systeminfo_cs.md#getEnvironmentVariable_cstr_cstr)*


## Texture Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***SAMPLER_SHADOW_COMPARE*** | Removed. |
| ***SAMPLER_SHADOW_MASK*** | Removed. |


## StructuredBuffer Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***USAGE_SHARED** = 1 << 3* | Value changed to 1 << 4. |


#### New Functions


- *[USAGE_DYNAMIC](../api/library/rendering/class.structuredbuffer_cs.md#USAGE_DYNAMIC)*


## UlonValue Class


#### New Functions


- *[**GetShort**( )](../api/library/common/class.ulonvalue_cs.md#getShort_short)*


## VR Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| Property ***HasFeatureTrackingSpaceRaw*** | Removed. |
| ***TRACKING_SPACE.UNKNOWN*** | Replaced with ***TRACKING_SPACE.LOCAL***. |
| ***TRACKING_SPACE.SEATED*** | Replaced with ***TRACKING_SPACE.LOCAL***. |
| ***TRACKING_SPACE.STANDING*** | Replaced with ***TRACKING_SPACE.ABSOLUTE***. |


#### New Properties


- *[**FoveatedFixedEyeCenterBias**](../api/library/vr/class.vr_cs.md#FoveatedFixedEyeCenterBias)*
- *[**AbsoluteToLocalWorldTransform**](../api/library/vr/class.vr_cs.md#AbsoluteToLocalWorldTransform)*


## ViewportData Class


#### New Functions


- *[WINDOW_MODE enumeration naming changed.](../api/library/plugins/spidervision/class.viewportdata_cs.md#WINDOW_MODE)*
- *[**RestoreBase**( Stream )](../api/library/plugins/spidervision/class.viewportdata_cs.md#restoreBase_Stream_void)*
- *[**SaveBase**( Stream )](../api/library/plugins/spidervision/class.viewportdata_cs.md#saveBase_Stream_void)*


## WallGroupData Class


#### New Properties


- *[**Aspect**](../api/library/plugins/spidervision/class.wallgroupdata_cs.md#Aspect)*
- *[**TransformType**](../api/library/plugins/spidervision/class.wallgroupdata_cs.md#TransformType)*
- *[**VFov**](../api/library/plugins/spidervision/class.wallgroupdata_cs.md#VFov)*


## WidgetVBox Class


#### New Functions


- *[**GetBackgroundBlendDestFunc**( )](../api/library/gui/class.widgetvbox_cs.md#getBackgroundBlendDestFunc_int)*
- *[**GetBackgroundBlendSrcFunc**( )](../api/library/gui/class.widgetvbox_cs.md#getBackgroundBlendSrcFunc_int)*
- *[**SetBackgroundBlendFunc**( int, int )](../api/library/gui/class.widgetvbox_cs.md#setBackgroundBlendFunc_int_int_void)*


## IG::Manager Class


#### New Properties


- *[**NEDConverter**](../api/library/plugins/ig/api/class.managerinterface_cs.md#NEDConverter)*


## IG::Entity Class


#### New Properties


- *[**OwnerID**](../api/library/plugins/ig/api/class.entity_cs.md#OwnerID)*
- *[**DebugDescription**](../api/library/plugins/ig/api/class.entity_cs.md#DebugDescription)*


## IG::NEDConverter Class


#### New Functions


- *[TARGET_COORDINATE_SYSTEM.NED](../api/library/plugins/ig/api/class.nedconverter_cs.md#TARGET_COORDINATE_SYSTEM_NED)*
- *[TARGET_COORDINATE_SYSTEM.ENU](../api/library/plugins/ig/api/class.nedconverter_cs.md#TARGET_COORDINATE_SYSTEM_ENU)*
- *[**ENUtoNED**( dvec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#ENUtoNED_dvec3_dvec3)*
- *[**NEDtoENU**( dvec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#NEDtoENU_dvec3_dvec3)*
- *[**TARGETtoENU**( dvec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#TARGETtoENU_dvec3_dvec3)*
- *[**ENUtoTARGET**( dvec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#ENUtoTARGET_dvec3_dvec3)*
- *[**ENUtoNED**( vec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#ENUtoNED_vec3_vec3)*
- *[**NEDtoENU**( vec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#NEDtoENU_vec3_vec3)*
- *[**TARGETtoENU**( vec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#TARGETtoENU_vec3_vec3)*
- *[**ENUtoTARGET**( vec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#ENUtoTARGET_vec3_vec3)*
- *[**EulerENUToRotation**( vec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#eulerENUToRotation_vec3_quat)*
- *[**EulerNEDToRotation**( vec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#eulerNEDToRotation_vec3_quat)*
- *[**EulerTARGETToRotation**( vec3 )](../api/library/plugins/ig/api/class.nedconverter_cs.md#eulerTARGETToRotation_vec3_quat)*
- *[**RotationToEulerENU**( quat )](../api/library/plugins/ig/api/class.nedconverter_cs.md#rotationToEulerENU_quat_vec3)*
- *[**RotationToEulerNED**( quat )](../api/library/plugins/ig/api/class.nedconverter_cs.md#rotationToEulerNED_quat_vec3)*
- *[**RotationToEulerTARGET**( quat )](../api/library/plugins/ig/api/class.nedconverter_cs.md#rotationToEulerTARGET_quat_vec3)*


#### New Properties


- *[**TargetCoordinateSystem**](../api/library/plugins/ig/api/class.nedconverter_cs.md#TargetCoordinateSystem)*
